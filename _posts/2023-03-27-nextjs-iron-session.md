---
layout: post
title: Next.js에서 iron-session을 이용해 세션 관리하기
description: iron-session으로 보완이 강화된 세션 처리
date: 2023-03-27
published : true
categories: next.js session
---

## iron session?
서명 및 암호화된 쿠키를 사용하여 데이터를 저장하는 Node.js의 stateless 세션 유틸리티이다. Next.js, Express 및 Node.js HTTP 서버에서 동작한다.
세션 데이터는 암호화된 쿠키(”seals”)에 저장된다. 그리고 사용중인 서버에서만 세션 데이터를 디코딩할 수 있다. iron session은 세션 ID가 없으므로 서버 관점에서 Iron 세션을 “무상태”로 만든다.

## Next.js에서 iron session과 Next API Route를 이용한 세션 토큰 처리
로그인 한 사용자의 정보를 iron session 라이브러리를 사용해 브라우저 쿠키에 암호환 된 형태로 저장했다.
먼저 사용자의 access token과 refresh token 갱신 관리를 하는 Next API Route를 `/api/user`로 만들었다. 그리고 클라이언트에서 특정 API를 호출하면 엔드포인트로 가기전에 Next API 안에서 토큰 상태를 확인하기 위해서 `/api/user`를 호출하려고 했다.
Next API Route에서 다시 또 다른 Next API Route에 요청을 하는 방식이다. 그런데 iron session은 특성상 request의 session에 데이터가 저장된다. request는 클라이언트에서 한다. 클라이언트에는 브라우저 세션에 있는 쿠키가 있다. API Route에서 `request.session`으로 데이터에 액세스가 가능하다.
하지만 API Route에서 API Route를 호출 하면 서버 to 서버가 되기 때문에 request에 session이 없다. 즉, req.session이 undefined가 나오는 이슈가 생긴다. API Route에서 다른 API Route에 요청을 날리는 건 바람직 하지 않다. 클라이언트 사이드에서 특정 시점마다 토큰을 갱신하는 API를 호출 하는 게 좋을 것 같다.
