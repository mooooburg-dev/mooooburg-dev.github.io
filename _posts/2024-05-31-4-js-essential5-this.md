---
layout: post
title: 자바스크립트에서 꼭 익혀야 할 5가지 개념 - 5.this
description: 함수가 호출 방식에 따라 다른 객체를 참조하는 조금은 특별한 키워드 this
date: 2024-05-31
published : true
categories: javascript
---

### this란?
`this`란 자바스크립트에서 현재 실행 중인 함수나 메서드가 속한 객체를 참조하는 특별한 키워드입니다. `this`가 참조하는 객체는 함수 호출 방식에 따라 달라집니다. ES5는 함수를 어떻게 호출했는지 상관하지 않고 this 값을 설정할 수 있는 bind 메서드를 도입했고, ES2015는 스스로의 this 바인딩을 제공하지 않는 화살표 함수를 추가했습니다(이는 렉시컬 컨텍스트안의 this값을 유지합니다).

### 다양한 `this` 바인딩 방식

1. **전역 컨텍스트**:
   - 전역 스코프에서 `this`는 전역 객체를 참조합니다.
   - 브라우저 환경에서는 `window` 객체를, Node.js 환경에서는 `global` 객체를 가리킵니다.

   ```javascript
   console.log(this); // 브라우저에서는 window 객체 출력
   ```

2. **함수 호출**:
   - 일반 함수 호출에서는 `this`가 전역 객체를 참조합니다 (엄격 모드에서는 `undefined`).

   ```javascript
   function regularFunction() {
     console.log(this);
   }

   regularFunction(); // 브라우저에서는 window 객체 출력 (엄격 모드에서는 undefined)
   ```

3. **메서드 호출**:
   - 객체의 메서드에서 `this`는 그 메서드를 호출한 객체를 참조합니다.

   ```javascript
   const obj = {
     name: 'Alice',
     greet: function() {
       console.log(this.name);
     }
   };

   obj.greet(); // 'Alice' 출력
   ```

4. **생성자 함수 호출**:
   - 생성자 함수에서 `this`는 새로 생성된 인스턴스 객체를 참조합니다.

   ```javascript
   function Person(name) {
     this.name = name;
   }

   const person = new Person('Bob');
   console.log(person.name); // 'Bob' 출력
   ```

5. **`call`, `apply`, `bind` 메서드 사용**:
   - `call`, `apply`, `bind` 메서드를 사용하여 `this`를 명시적으로 지정할 수 있습니다.

   ```javascript
   function sayName() {
     console.log(this.name);
   }

   const obj = { name: 'Charlie' };

   sayName.call(obj); // 'Charlie' 출력
   ```

이와 같이 `this`는 함수가 호출되는 방식에 따라 다르게 바인딩되므로, 이를 이해하고 사용하는 것이 중요합니다.