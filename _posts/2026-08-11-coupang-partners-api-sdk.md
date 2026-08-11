---
layout: post
title: 쿠팡 파트너스 API 연동, SDK로 5분 만에 시작하기
description: 쿠팡 파트너스 API의 HMAC 서명 인증부터 상품 검색·GoldBox·딥링크·리포트까지, 직접 만든 오픈소스 TypeScript SDK(coupang-partners-sdk-standalone)로 간단하게 연동하는 방법을 정리했습니다.
date: 2026-08-11
published: true
categories: API TypeScript 오픈소스 사이드프로젝트
---

> 📦 npm 패키지 → [**coupang-partners-sdk-standalone**](https://www.npmjs.com/package/coupang-partners-sdk-standalone){:target="\_blank" rel="noopener"}<br>
> 🧪 브라우저에서 바로 테스트 → [**Test Console 데모**](https://cp-sdk-console.vercel.app){:target="\_blank" rel="noopener"}

## 네 줄 요약

- 쿠팡 파트너스 API는 **HMAC SHA256 CEA 서명**을 매 요청마다 직접 만들어야 해서 진입 장벽이 있다
- 이 서명·인증·에러 처리를 감싼 오픈소스 SDK **`coupang-partners-sdk-standalone`** 를 npm에 공개했다
- **상품 검색 · GoldBox · CoupangPL · 딥링크 · 리포트** API를 TypeScript 타입과 함께 바로 호출할 수 있다
- 코드 없이 응답을 먼저 확인하고 싶다면 [**Test Console**](https://cp-sdk-console.vercel.app){:target="\_blank" rel="noopener"} 웹 데모에서 실시간으로 테스트할 수 있다

---

## 1. 쿠팡 파트너스 API가 까다로운 이유

쿠팡 파트너스(Coupang Partners) API로 제휴 마케팅을 붙이려면 생각보다 손이 많이 갑니다. 가장 큰 벽은 **인증**입니다.

모든 요청에는 `Authorization` 헤더에 **HMAC SHA256 기반 CEA 서명**을 넣어야 하는데, 이 서명은 다음을 조합해서 매 요청마다 새로 계산해야 합니다.

- HTTP 메서드 (`GET`, `POST`)
- 요청 경로 + 쿼리스트링
- 요청 시각(GMT, `yyMMdd'T'HHmmss'Z'` 포맷)
- Access Key / Secret Key

여기에 더해 응답이 항상 JSON인 것도 아니고(에러 시 HTML이 내려오기도 함), 네트워크 오류 재시도, 리포트 API의 날짜 포맷(`yyyyMMdd`) 제약까지 신경 써야 합니다. 매번 프로젝트마다 이 보일러플레이트를 다시 짜는 게 아까워서 SDK로 분리했습니다.

---

## 2. 설치

```bash
npm install coupang-partners-sdk-standalone
```

```bash
yarn add coupang-partners-sdk-standalone
```

TypeScript 타입이 내장되어 있어 별도 `@types` 설치가 필요 없습니다.

---

## 3. 기본 사용법

### 클라이언트 생성

```typescript
import { CoupangPartnersClient } from 'coupang-partners-sdk-standalone';

const client = new CoupangPartnersClient({
  accessKey: process.env.COUPANG_ACCESS_KEY!,
  secretKey: process.env.COUPANG_SECRET_KEY!,
});
```

서명 생성은 SDK가 내부적으로 처리하므로, 위 한 줄이면 준비가 끝납니다.

### 상품 검색

```typescript
const searchResult = await client.searchProducts('아이폰', {
  limit: 10,
  imageSize: '230x230',
});

if (searchResult.rCode === '0') {
  const products = searchResult.data?.productData ?? [];
  products.forEach((p) => {
    console.log(`${p.productName} - ₩${p.productPrice.toLocaleString()}`);
  });
}
```

### GoldBox 특가 상품

```typescript
const goldbox = await client.goldbox({
  subId: 'my-tracking-id',
  imageSize: '300x300',
});
```

### 딥링크(제휴 링크) 생성

일반 쿠팡 상품 URL을 추적 가능한 제휴 링크로 변환합니다.

```typescript
const deeplink = await client.deeplink({
  coupangUrls: ['https://www.coupang.com/vp/products/184614775'],
  subId: 'my-tracking-id',
});

deeplink.data?.forEach((link) => {
  console.log(link.shortenUrl); // 단축 제휴 링크
});
```

### 실적 리포트

일별 클릭·주문·수익·취소 실적을 조회할 수 있습니다. (실적은 매일 오후 15:00에 갱신)

```typescript
const clicks = await client.getClicksReport({
  startDate: '20260801', // yyyyMMdd
  endDate: '20260811', // 시작일과 30일 이내
});
```

---

## 4. 지원하는 API 한눈에 보기

| 메서드                               | 설명                                       |
| ------------------------------------ | ------------------------------------------ |
| `searchProducts()`                   | 키워드 상품 검색                           |
| `goldbox()` / `goldboxWithFilters()` | GoldBox 특가 상품 조회(+클라이언트 필터링) |
| `coupangPL()`                        | CoupangPL 상품 조회                        |
| `deeplink()`                         | 딥링크(제휴 링크) 생성                     |
| `getClicksReport()`                  | 일별 클릭 리포트                           |
| `getOrdersReport()`                  | 일별 주문 리포트                           |
| `getCommissionReport()`              | 일별 수익 리포트                           |
| `getCancelsReport()`                 | 일별 취소 리포트                           |

에러 핸들링(HTTP/JSON 파싱), 자동 재시도, 디버그 로깅, 타임아웃 설정 등 부가 기능도 옵션으로 제공합니다.

```typescript
const client = new CoupangPartnersClient(
  { accessKey, secretKey },
  { timeout: 15000, debug: true },
);
```

---

## 5. 코드 없이 먼저 테스트해 보기

"내 API 키로 어떤 응답이 오는지"를 코드 작성 전에 확인하고 싶을 때가 있습니다. 그래서 SDK를 그대로 호출하는 웹 데모, **쿠팡 파트너스 API Test Console**을 함께 만들었습니다.

- 🧪 데모: [cp-sdk-console.vercel.app](https://cp-sdk-console.vercel.app){:target="\_blank" rel="noopener"}
- 📖 프로젝트 소개: [drawyourmind.com/works/cp-sdk-console](https://drawyourmind.com/works/cp-sdk-console){:target="\_blank" rel="noopener"}

상품 검색·GoldBox·CoupangPL·딥링크를 UI에서 파라미터를 바꿔가며 실시간으로 호출하고, 응답을 상품 카드로 시각화해서 볼 수 있습니다.

---

## 6. 링크 정리

- 📦 **npm**: <https://www.npmjs.com/package/coupang-partners-sdk-standalone>
- 💻 **GitHub**: <https://github.com/mooooburg-dev/coupang-partners-sdk-standalone>
- 🧪 **Test Console(데모)**: <https://cp-sdk-console.vercel.app>
- 📖 **프로젝트 상세**: <https://drawyourmind.com/works/cp-sdk-console>

버그 리포트나 기능 요청은 [GitHub Issues](https://github.com/mooooburg-dev/coupang-partners-sdk-standalone/issues){:target="\_blank" rel="noopener"}로 남겨주시면 감사하겠습니다. ⭐ Star도 언제나 환영합니다.
