---
layout: post
title: 기획전 페이지에 이벤트 기간 가드 적용하기
description: SSR/CSR 양쪽에서 기획전 기간을 체크하여 종료된 이벤트의 데이터 노출과 불필요한 fetch를 차단한 경험
date: 2026-05-21
published: true
categories: Next.js TypeScript
---

## 한 줄 요약

기획전(Exhibition) 페이지에서 **이벤트 기간이 아닌데도 콘텐츠가 그대로 렌더링되는 문제**를 발견하고, SSR·CSR 양쪽에서 기간 가드를 적용한 기록입니다.

---

## 1. 문제 발견

홈쇼핑모아의 큐레이션 기획전 페이지(`/event?id=xxx`)는 CMS에서 `production: true`를 켜면 노출되는 구조입니다. 그런데 이미 종료된 기획전도 화면이 정상적으로 렌더되고 있었습니다.

원인을 추적해보니, **기획전 레벨의 기간 체크가 아예 없었습니다.**

```typescript
// 기존 코드 — stage/production 플래그만 체크
if (isStage() || isDevelopment()) {
  isEventActive = data.stage === true;
} else if (isProd()) {
  isEventActive = data.production === true;
}
```

개별 컴포넌트에는 `start_datetime`/`end_datetime` 기반 시간 필터링이 있었지만, 기획전 자체의 시작·종료 시각은 확인하지 않고 있었습니다. 즉 `production: true`이기만 하면 시작 전이든 종료 후든 무조건 노출.

---

## 2. 설계 시 고려한 포인트

단순히 UI 분기만 추가하면 끝이 아니었습니다. 세 가지 리스크를 함께 잡아야 했습니다.

### SSR 데이터 노출

Next.js Pages Router의 `getServerSideProps`에서 반환하는 props는 `__NEXT_DATA__` 스크립트 태그에 그대로 직렬화됩니다. 기간이 지난 기획전이라도 `initialEventData`나 `productPools`가 props에 담기면 클라이언트 소스에 실데이터가 노출됩니다.

### CSR fetch 실행

`EventContent` 컴포넌트의 `useEffect`가 `isEventActive`만 보고 fetch를 트리거하고 있어서, 기간 외 상태에서도 API 호출이 발생할 수 있었습니다.

### 시간 비교 안정성

기존 컴포넌트 레벨 시간 체크에서 사용하던 패턴이 있었는데:

```typescript
const now = new Date(
  new Date().toLocaleString('en-US', { timeZone: 'Asia/Seoul' }),
);
```

`toLocaleString`으로 KST 문자열을 만든 뒤 다시 `new Date()`로 파싱하는 이중 변환인데, 서버 런타임의 로케일 설정에 따라 파싱 결과가 달라질 수 있는 방식이었습니다.

---

## 3. 구현

### 시간 유틸리티 함수

`utils/timeFilter.ts`에 두 함수를 추가했습니다.

```typescript
// KST datetime 문자열을 UTC 밀리초 timestamp로 파싱
// 타임존 정보가 없으면 +09:00(KST) 붙여서 변환
export function parseKSTDatetime(datetime: string): number {
  const trimmed = datetime.trim();
  const hasTimezone =
    /[Z+\-]\d{2}:\d{2}$/.test(trimmed) || trimmed.endsWith('Z');
  return hasTimezone
    ? new Date(trimmed).getTime()
    : new Date(`${trimmed}+09:00`).getTime();
}

// 현재 시각이 기간 내인지 판정
// 경계값 포함: start <= now <= end
// 파싱 실패 시 false 반환 (fail-closed)
export function isWithinPeriod(
  startDatetime?: string | null,
  endDatetime?: string | null,
): boolean {
  if (!startDatetime && !endDatetime) return true;

  const now = Date.now();

  if (startDatetime) {
    const startTs = parseKSTDatetime(startDatetime);
    if (Number.isNaN(startTs)) return false;
    if (now < startTs) return false;
  }
  if (endDatetime) {
    const endTs = parseKSTDatetime(endDatetime);
    if (Number.isNaN(endTs)) return false;
    if (now > endTs) return false;
  }
  return true;
}
```

**fail-closed 원칙** — 파싱이 실패하면 "기간 내"가 아닌 "기간 외"로 처리합니다. 기간 차단 로직이므로 실패 시 열리는 것보다 닫히는 게 안전합니다.

기존에 컴포넌트 엘리먼트 필터링에 쓰이던 `filterElementsByTime`도 `isWithinPeriod`를 재사용하도록 통합했습니다.

```typescript
export function filterElementsByTime<T extends Record<string, any>>(
  elements: T[],
): T[] {
  return elements.filter((element) =>
    isWithinPeriod(element.start_datetime, element.end_datetime),
  );
}
```

### SSR — getServerSideProps

```typescript
// 기획전 기간 체크
if (isEventActive) {
  isEventPeriod = isWithinPeriod(data.start_datetime, data.end_datetime);
}

// 기간 내에만 데이터 할당
if (isEventActive && isEventPeriod && data.product_pool) {
  productPools = data.product_pool;
}
if (isEventActive && isEventPeriod && data.components) {
  initialEventData = data.components;
  // ... headerComponent 추출
}
```

`isEventPeriod`가 `false`이면 `initialEventData`와 `productPools`가 빈 상태로 남아, `__NEXT_DATA__`에 실데이터가 포함되지 않습니다.

### CSR — useEffect fetch 차단

```typescript
// 기간 내에만 fetch 실행
if (isEventActive && isEventPeriod) {
  const eventIdToUse = eventId || DEFAULT_EVENT_ID;
  if (!initialEventData) {
    fetchEventData(eventIdToUse);
  }
  setEventId(eventIdToUse);
} else {
  setLoading(false);
}
```

### 안내 화면

```tsx
if (!isEventPeriod) {
  return (
    <div className="flex h-screen items-center justify-center">
      <div className="text-center">
        <p className="mb-2 text-gray-500">이벤트 기간이 아닙니다.</p>
        {exhibition && (
          <p className="text-sm text-gray-400">{exhibition.exhibition_title}</p>
        )}
      </div>
    </div>
  );
}
```

---

## 4. 테스트

Jest로 `isWithinPeriod`의 경계 케이스를 검증했습니다.

```
✓ 둘 다 없으면 true
✓ start만 있고 현재가 start 이후 → true
✓ start만 있고 현재가 start 이전 → false
✓ end만 있고 현재가 end 이전 → true
✓ end만 있고 현재가 end 이후 → false
✓ 기간 내 → true
✓ 기간 외 (시작 전) → false
✓ 기간 외 (종료 후) → false
✓ start와 정확히 같은 시각 → true (경계값 포함)
✓ end와 정확히 같은 시각 → true (경계값 포함)
✓ start 파싱 실패 → false
✓ end 파싱 실패 → false
✓ 둘 다 파싱 실패 → false
```

`jest.useFakeTimers()`로 시스템 시각을 고정하고, 경계값 포함(`==`)과 파싱 실패 시 `false` 반환을 모두 확인했습니다.

---

## 5. 기간 판정 정리

| 조건           | 결과                              |
| -------------- | --------------------------------- |
| `start`만 있음 | `now >= start`이면 기간 내        |
| `end`만 있음   | `now <= end`이면 기간 내          |
| 둘 다 있음     | `start <= now <= end`이면 기간 내 |
| 둘 다 없음     | 항상 기간 내 (기존 동작 유지)     |
| 파싱 실패      | 기간 외 (fail-closed)             |

---

## 6. 돌아보며

처음에는 "종료된 이벤트가 보인다"는 단순한 버그로 시작했지만, 파고 들어가 보니 UI 분기 하나로 끝날 문제가 아니었습니다.

- **데이터가 내려오는 것 자체가 문제** — 화면을 숨겨도 `__NEXT_DATA__`에 남아 있으면 의미 없음
- **CSR fetch도 별도로 막아야 함** — SSR에서 데이터를 안 내려줘도 클라이언트가 알아서 다시 가져옴
- **시간 비교는 생각보다 까다로움** — `toLocaleString` 이중 파싱은 서버 환경에 따라 결과가 달라질 수 있음
- **실패 시 기본값 방향이 중요** — 차단 로직이라 fail-open이면 무방비 상태가 됨

"UI만 가리면 되겠지"라고 넘어갈 수 있는 부분인데, SSR 프레임워크에서는 렌더링과 데이터 전달이 별개 레이어라는 점을 다시 한번 느꼈습니다.
