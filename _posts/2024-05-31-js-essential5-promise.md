---
layout: post
title: 자바스크립트에서 꼭 익혀야 할 5가지 개념 - 2.Promise
description: Promise는 비동기 작업의 완료 또는 실패를 처리하기 위한 자바스크립트 객체입니다.
date: 2024-05-31
published : true
categories: javascript
---

### Promise란?
Promise는 JavaScript에서 비동기 작업을 처리하기 위해 사용되는 객체입니다. 비동기 작업이 완료된 후 그 결과를 처리하는 방법을 제공하며, 콜백 함수의 중첩으로 인한 복잡성을 줄여줍니다. Promise는 주로 다음 세 가지 상태를 가집니다.

1. **Pending(대기)**: 초기 상태로, 비동기 작업이 아직 완료되지 않은 상태입니다.
2. **Fulfilled(이행)**: 비동기 작업이 성공적으로 완료되어 결과 값을 반환한 상태입니다.
3. **Rejected(거부)**: 비동기 작업이 실패하여 에러를 반환한 상태입니다.

Promise는 `then()`, `catch()`, `finally()` 메서드를 통해 비동기 작업의 성공, 실패, 완료 후 처리할 작업을 정의할 수 있습니다.

예제를 통해 Promise의 기본 사용법을 살펴보겠습니다.

```javascript
// Promise 생성
const myPromise = new Promise((resolve, reject) => {
  let success = true; // 성공 여부를 나타내는 변수
  if (success) {
    resolve("작업이 성공적으로 완료되었습니다!");
  } else {
    reject("작업에 실패했습니다.");
  }
});

// Promise 사용
myPromise
  .then((message) => {
    console.log(message); // 성공 시 메시지 출력: "작업이 성공적으로 완료되었습니다!"
  })
  .catch((error) => {
    console.error(error); // 실패 시 에러 메시지 출력: "작업에 실패했습니다."
  })
  .finally(() => {
    console.log("작업이 완료되었습니다."); // 성공 여부와 관계없이 실행
  });
```

이 예제에서 `myPromise`는 비동기 작업을 나타내며, `resolve` 함수는 작업이 성공적으로 완료되었음을 나타내고, `reject` 함수는 작업이 실패했음을 나타냅니다. `then()` 메서드는 작업이 성공했을 때 실행될 콜백을 지정하고, `catch()` 메서드는 작업이 실패했을 때 실행될 콜백을 지정하며, `finally()` 메서드는 작업의 성공 여부와 상관없이 항상 실행됩니다.

Promise는 비동기 작업의 체인(chain)을 구성할 수 있어, 여러 비동기 작업을 순차적으로 실행하거나 병렬로 실행한 후 결과를 처리하는 데 유용합니다. 예를 들어, 다음과 같은 방식으로 Promise를 체인으로 연결할 수 있습니다:

```javascript
const promise1 = new Promise((resolve) => setTimeout(() => resolve(1), 1000));
const promise2 = new Promise((resolve) => setTimeout(() => resolve(2), 2000));
const promise3 = new Promise((resolve) => setTimeout(() => resolve(3), 3000));

Promise.all([promise1, promise2, promise3])
  .then((values) => {
    console.log(values); // [1, 2, 3]
  })
  .catch((error) => {
    console.error(error);
  });
```

이 예제에서는 `Promise.all` 메서드를 사용하여 여러 Promise를 병렬로 실행하고, 모든 Promise가 완료되면 결과를 배열로 반환합니다. 이를 통해 효율적으로 비동기 작업을 관리할 수 있습니다.