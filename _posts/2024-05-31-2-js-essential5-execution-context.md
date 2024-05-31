---
layout: post
title: 자바스크립트에서 꼭 익혀야 할 5가지 개념 - 3.실행 컨텍스트
description: 자바스크립트 코드가 실행되는 동안 변수, 함수, 객체의 유효 범위와 this 바인딩을 관리하는 환경입니다.
date: 2024-05-31
published : true
categories: javascript
---

### 실행 컨텍스트란?
실행 컨텍스트(Execution Context)는 자바스크립트 코드가 실행될 때 생성되는 환경으로, 변수, 함수, 객체 등이 어떻게 실행되고 저장될지 결정하는 중요한 개념입니다. 실행 컨텍스트는 크게 세 가지 유형으로 나뉩니다.

1. **전역 실행 컨텍스트(Global Execution Context)**:
   - 자바스크립트 코드가 처음 실행될 때 생성됩니다.
   - 전역 객체(window 또는 global)와 `this`가 포함됩니다.
   - 전역 컨텍스트에서는 전역 변수와 함수를 관리합니다.

2. **함수 실행 컨텍스트(Function Execution Context)**:
   - 함수가 호출될 때마다 생성됩니다.
   - 함수의 지역 변수, 인수(arguments), `this`, 그리고 새로운 스코프 체인을 포함합니다.
   - 함수 실행이 끝나면 해당 컨텍스트는 사라집니다.

3. **Eval 실행 컨텍스트(Eval Execution Context)**:
   - `eval` 함수가 호출될 때 생성됩니다.
   - 일반적으로 사용하지 않으며, 권장되지 않는 방식입니다.

### 실행 컨텍스트의 구성 요소
실행 컨텍스트는 세 가지 주요 구성 요소로 이루어져 있습니다.

1. **변수 객체(Variable Object, VO)**:
   - 실행 컨텍스트 내에서 선언된 변수, 함수 선언, 함수의 매개변수를 포함합니다.
   - 전역 컨텍스트에서는 전역 객체와 동일하며, 함수 컨텍스트에서는 활성화 객체(Activation Object, AO)로 변환됩니다.

2. **스코프 체인(Scope Chain)**:
   - 현재 컨텍스트와 부모 컨텍스트의 변수 객체를 연결하여 변수와 함수를 검색하는 데 사용됩니다.
   - 함수가 중첩될 때 부모 함수의 스코프를 참조하여 변수를 찾습니다.

3. **this 바인딩(this Binding)**:
   - 실행 컨텍스트에서 `this`가 가리키는 객체를 정의합니다.
   - 전역 컨텍스트에서는 전역 객체를, 함수 컨텍스트에서는 함수 호출 방식에 따라 다르게 바인딩됩니다.

### 예제
실행 컨텍스트를 이해하기 위한 간단한 예제를 살펴보겠습니다.

```javascript
var globalVar = "I am a global variable";

function outerFunction() {
  var outerVar = "I am an outer variable";

  function innerFunction() {
    var innerVar = "I am an inner variable";
    console.log(globalVar); // "I am a global variable"
    console.log(outerVar);  // "I am an outer variable"
    console.log(innerVar);  // "I am an inner variable"
  }

  innerFunction();
}

outerFunction();
```

이 예제에서 실행 컨텍스트의 흐름은 다음과 같습니다.

1. **전역 실행 컨텍스트**:
   - `globalVar` 변수가 전역 객체에 등록됩니다.
   - `outerFunction` 함수가 전역 객체에 등록됩니다.

2. **`outerFunction` 실행 컨텍스트**:
   - `outerVar` 변수가 `outerFunction`의 변수 객체에 등록됩니다.
   - `innerFunction` 함수가 `outerFunction`의 변수 객체에 등록됩니다.

3. **`innerFunction` 실행 컨텍스트**:
   - `innerVar` 변수가 `innerFunction`의 변수 객체에 등록됩니다.
   - `globalVar`와 `outerVar`는 스코프 체인을 통해 접근됩니다.

이러한 실행 컨텍스트의 구조 덕분에 자바스크립트는 변수와 함수의 유효 범위를 결정하고, 함수 호출 시 정확한 `this` 바인딩을 설정할 수 있습니다.