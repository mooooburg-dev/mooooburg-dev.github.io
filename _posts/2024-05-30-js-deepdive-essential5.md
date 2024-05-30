---
layout: post
title: 자바스크립트에서 꼭 익혀야 할 5가지 개념 - 1.스코프(Scope)
description: 스코프는 변수나 함수가 접근할 수 있는 유효 범위를 의미합니다.
date: 2024-05-30
published : true
categories: javascript
---

### 스코프란?
스코프는 변수나 함수가 접근할 수 있는 유효 범위를 의미합니다. 자바스크립트에서는 주로 두 가지 스코프가 있습니다.
1. **전역 스코프(Global Scope)**
   - 코드 어디서나 접근할 수 있는 범위입니다.
   - 전역 스코프에 선언된 변수나 함수는 프로그램 전체에서 사용할 수 있습니다.
      ```js
      var globalVar = "나는 전역 변수입니다";

      function globalFunction() {
        console.log(globalVar);
      }

      globalFunction(); // "나는 전역 변수입니다" 출력
      ```
2. **지역 스코프(Local Scope)**
   - 특정 함수나 블록 내에서만 유효한 범위입니다.
   - 지역 스코프에 선언된 변수나 함수는 해당 범위 내에서만 접근할 수 있습니다.
      ```js
      function localScope() {
        var localVar = "나는 지역 변수입니다";
        console.log(localVar);
      }

      localScope(); // "나는 지역 변수입니다" 출력
      console.log(localVar); // 오류 발생: localVar는 정의되지 않음
      ```

### 블록 스코프(Block Scope)
자바스크립트에서는 `let`과 `const` 키워드를 사용하여 블록 스코프를 생성할 수 있습니다. 블록 스코프는 `{}` 중괄호로 감싸인 범위 내에서만 유효합니다.
```javascript
if (true) {
  let blockVar = "나는 블록 변수입니다";
  console.log(blockVar); // "나는 블록 변수입니다" 출력
}

console.log(blockVar); // 오류 발생: blockVar는 정의되지 않음
```

### 요약
- **전역 스코프**: 코드 어디서나 접근 가능한 범위
- **지역 스코프**: 함수 내에서만 접근 가능한 범위
- **블록 스코프**: 블록(`{}`) 내에서만 접근 가능한 범위(`let`, `const` 사용 시)

이렇게 스코프를 이해하면 변수가 함수의 유효 범위를 효과적으로 관리할 수 있습니다.

### Promise


### 실행컨텍스트


### 호출스택


### this

