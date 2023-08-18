---
layout: post
title: 자바스크립트로 라이브러리 없이 UUID 함수 만들기
description: UUID 요약 및 생성 방법
date: 2023-08-18
published : true
categories: js, uuid
---

## UUID(Universally Unique IDentifier)란?
- `UUID`는 정보 식별을 위하여 사용되는 식별자다.
- 128-bit 숫자로 이루어져 있으며, xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxxx 형식으로 표현한다.
- UUID의 장점 중, 데이터들이 나중에 단일 DB로 통합되거나, 같은 채널에서 전송되더라도 식별자가 중복될 확률이 매우 낮다는 점이 있다.

## Generate a UUID in JS
자바스크립트에서 UUID를 생성할 수 있는 다양한 방법이 존재한다. 대표적으로 [randomUUID()](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID) 메소드를 사용할 수 있다.
```js
/* Assuming that self.crypto.randomUUID() is available */

let uuid = self.crypto.randomUUID();
console.log(uuid); // for example "36b8f84d-df4e-4d49-b662-bcde71a8764f"
```
하지만 보안 정책으로 인해 `HTTPS` 프로토콜과 `localhost` 테스트 환경에서만 동작한다. 외부 라이브러리를 사용할 수 없거나 바닐라 스크립트로 코드를 작성해야만 하는 상황이 생길 수 있어서 아래와 같은 함수가 필요한 경우가 있을 수 있다.

## Javascript로 UUID 생성하기
```js
function uuidv4() {
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
    return v.toString(16);
  });
}

console.log(uuidv4())
// 2ea29c0f-d031-4e62-80e8-1fadadbd009e
```

```js
function guid() {
  function _s4() {
    return ((1 + Math.random()) * 0x10000 | 0).toString(16).substring(1);
  }
  return _s4() + _s4() + '-' + _s4() + '-' + _s4() + '-' + _s4() + '-' + _s4() + _s4() + _s4();
}

console.log(guid())
// 90cc61a4-0bfc-4422-f029-85a6b85937c7
```



