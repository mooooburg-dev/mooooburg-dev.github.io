---
layout: post
title: Next.js에서 iron-session을 이용해 세션 관리하기
description: iron-session으로 보완을 강화된 세션 처리
date: 2023-03-27
published : true
categories: next.js session
---

## iron session?
서명 및 암호화된 쿠키를 사용하여 데이터를 저장하는 Node.js의 stateless 세션 유틸리티이다. Next.js, Express 및 Node.js HTTP 서버에서 동작한다.
세션 데이터는 암호화된 쿠키(”seals”)에 저장된다. 그리고 사용중인 서버에서만 세션 데이터를 디코딩할 수 있다. iron session은 세션 ID가 없으므로 서버 관점에서 Iron 세션을 “무상태”로 만든다.

## 동작 방식
1. 브라우저가 서버에 요청을 보냄.
2. 서버에서 정보를 암호화한 쿠키를 만듦.
3. 브라우저에게 응답을 보낼 때 쿠키를 같이 보냄.
4. 브라우저는 암호화된 쿠키를 가지고, 이후 요청에 쿠키를 같이 보내짐.
5. 암호화된 쿠키를 받은 서버는 이를 복호화해 정보를 활용함.

## 장점
1. JWT가 아니다. 암호화 되어 유저가 정보를 확인할 수 없다.
2. 세션을 위한 백엔드를 구축하지 않아도 된다.
3. 유용한 `helper function = withIronSessionApiRoute`가 있다.


```javascript
// withIronSesstionApiRoute로 handler를 감싸준다
export default withIronSesstionApiRoute(
  // 👇 handler
  async function loginRoute(req, res) {
    req.session.user = {
      id: 1,
      admin : true,
    };
    await req.session.save();
    res.send({ok: true});
  }
)
// Promise를 return 한다.
```


- `withIronSessionApiRoute`를 통해서 감싸진 handler의 request 객체에 session 객체를 담아서 쿠키로 보내지게 된다.  
- `withHandler`와 같이 사용하면 아래와 같이 작성한다.


```javascript
export default withIronSesstionApiRoute(withHandler("POST", handler), {
  cookieName : "carrotsession",
  password : "thisisthesomethingpassword" //password를 통해서 쿠키를 암호화/복호화한다.
});
```

## Next.js에서 iron session과 Next API Route를 이용한 토큰 처리
로그인 한 사용자의 정보를 iron session 라이브러리를 사용해 브라우저 쿠키에 암호환 된 형태로 저장한다. 먼저 사용자의 `access token`과 `refresh token` 갱신 관리를 하는 Next API Route를 `/api/user`로 만들었다. 그리고 클라이언트에서 특정 API를 호출하면 엔드포인트까지 가기전에 Next API 안에서 토큰 상태를 확인하기 위해서 `/api/user`를 거치도록 했다.  
  
즉 Next API Route(토큰 상태 확인)에서 다시 또 다른 Next API Route(실제 호출하는 API)에 요청을 하는 방식이다. 그런데 iron session은 `request`객체 의 `session` 안에 데이터가 저장된다. 요청 request는 클라이언트로에서 시작 된다. 클라이언트에는 브라우저 세션에 있는 쿠키에 접근이 가능하다. 즉 Next API Route에서 `request.session`으로 데이터에 액세스가 가능하다.
  
하지만 Next API Route에서 또 다른 Next API Route를 호출하게 되면 서버 to 서버가 되기 때문에 request 객체 안에 session이 없다. 즉, req.session이 undefined가 나오는 이슈가 생긴다. 그리고 iron session의 데이터는 사용중인 서버에서만 디코딩을 할 수 있다고 하는데 API Route에서 다른 API Route에 요청을 보낼 때 디코딩이 가능한 지 확인을 못했다. 토큰 처리는 클라이언트 사이드에서 토큰 관리 API를 직접 호출하는 것으로 해결했다.
