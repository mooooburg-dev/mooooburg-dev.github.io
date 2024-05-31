---
layout: post
title: 자바스크립트에서 꼭 익혀야 할 5가지 개념 - 4.호출 스택
description: 자바스크립트 엔진이 함수 호출을 관리하고 실행 순서를 제어하기 위해 사용하는 LIFO(후입선출) 구조의 자료 구조
date: 2024-05-31
published : true
categories: javascript
---

호출 스택(Call Stack)은 자바스크립트 엔진이 함수 호출을 관리하고 실행 흐름을 제어하는 데 사용하는 자료 구조입니다. 호출 스택은 LIFO(Last In, First Out) 구조로 동작하며, 가장 마지막에 추가된 항목이 가장 먼저 제거됩니다. 호출 스택의 주요 역할은 실행 컨텍스트를 관리하는 것입니다.

### 호출 스택의 동작 원리
1. **함수 호출**:
   - 함수가 호출되면 해당 함수의 실행 컨텍스트가 생성되고 호출 스택에 추가됩니다.
2. **함수 실행**:
   - 함수의 실행이 끝나면 해당 함수의 실행 컨텍스트가 호출 스택에서 제거됩니다.
3. **스택 비우기**:
   - 모든 함수 호출이 완료되면 호출 스택은 비어 있게 됩니다.

### 호출 스택 예제
간단한 예제를 통해 호출 스택의 동작을 이해해 보겠습니다:

```javascript
function firstFunction() {
  console.log("First Function");
  secondFunction();
}

function secondFunction() {
  console.log("Second Function");
  thirdFunction();
}

function thirdFunction() {
  console.log("Third Function");
}

firstFunction();
```

이 코드를 실행할 때 호출 스택의 상태 변화를 살펴보면 다음과 같습니다:

1. **초기 상태**:
   - 호출 스택은 비어 있습니다.

2. **`firstFunction` 호출**:
   - `firstFunction` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction]`

3. **`firstFunction` 실행 중 `console.log` 호출**:
   - `console.log` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction, console.log]`
   - `console.log` 실행 완료 후 호출 스택에서 제거됩니다.
   - 호출 스택: `[firstFunction]`

4. **`secondFunction` 호출**:
   - `secondFunction` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction, secondFunction]`

5. **`secondFunction` 실행 중 `console.log` 호출**:
   - `console.log` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction, secondFunction, console.log]`
   - `console.log` 실행 완료 후 호출 스택에서 제거됩니다.
   - 호출 스택: `[firstFunction, secondFunction]`

6. **`thirdFunction` 호출**:
   - `thirdFunction` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction, secondFunction, thirdFunction]`

7. **`thirdFunction` 실행 중 `console.log` 호출**:
   - `console.log` 실행 컨텍스트가 호출 스택에 추가됩니다.
   - 호출 스택: `[firstFunction, secondFunction, thirdFunction, console.log]`
   - `console.log` 실행 완료 후 호출 스택에서 제거됩니다.
   - 호출 스택: `[firstFunction, secondFunction, thirdFunction]`

8. **`thirdFunction` 실행 완료**:
   - `thirdFunction` 실행 컨텍스트가 호출 스택에서 제거됩니다.
   - 호출 스택: `[firstFunction, secondFunction]`

9. **`secondFunction` 실행 완료**:
   - `secondFunction` 실행 컨텍스트가 호출 스택에서 제거됩니다.
   - 호출 스택: `[firstFunction]`

10. **`firstFunction` 실행 완료**:
    - `firstFunction` 실행 컨텍스트가 호출 스택에서 제거됩니다.
    - 호출 스택: `[]`

### 호출 스택의 중요성
호출 스택은 자바스크립트 코드의 실행 흐름을 관리하고 디버깅할 때 매우 중요합니다. 특히, 재귀 함수가 너무 깊어지면 호출 스택이 초과되어 "스택 오버플로(Stack Overflow)" 에러가 발생할 수 있습니다. 이러한 문제를 예방하기 위해 호출 스택의 크기를 염두에 두고 코드를 작성하는 것이 좋습니다.