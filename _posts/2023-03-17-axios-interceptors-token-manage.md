---
layout: post
title: axios interceptors를 이용해서 token 관리
description: axios로 access token, refresh token 처리하기
date: 2023-03-17
published : true
categories: axios
---

# Axios Interceptor란?
Axios Interceptor는 axios의 `request`와 `response`를 가로채 필요한 기능을 추가할 수 있다.
axios의 return type이 Promise인 점을 이용해 특정 요청 전 부가 작업을 할 수 있게 해주는 라이브러리이다.

## Request Interceptor
http `request`가 서버에 전달되기 전에 호출 된다. 요청 헤더 및 인증, 로깅 등을 위해서 사용한다.

## Resoponse Interceptor
서버에 보낸 요청에 대한 response를 받은 후 `then` 또는 `catch`로 전달되기 전에 호출 된다.

## UseCase
```js
// 요청 인터셉터 추가
axios.interceptors.request.use(
  function (config) {
    // 요청을 보내기 전에 수행할 일
    // ...
    return config;
  },
  function (error) {
    // 오류 요청을 보내기전 수행할 일
    // ...
    return Promise.reject(error);
  });

// 응답 인터셉터 추가
axios.interceptors.response.use(
  function (response) {
    // 응답 데이터를 가공
    // ...
    return response;
  },
  function (error) {
    // 오류 응답을 처리
    // ...
    return Promise.reject(error);
  });
```

인터셉터를 제거(Eject) 해야 할 수도 있다.

```js
const myInterceptor = axios.interceptors.request.use(function () { /*...*/ });
axios.interceptors.request.eject(myInterceptor);
```

사용자 정의 axios 인스턴스에 인터셉터를 추가 할 수 있다.

```js
const instance = axios.create();
instance.interceptors.request.use(function () { /*...*/ });
```

