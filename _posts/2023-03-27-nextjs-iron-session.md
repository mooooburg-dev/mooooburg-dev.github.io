---
layout: post
title: Next.js에서 iron-session을 이용해 세션 관리하기
description: iron-session으로 보완이 강화된 세션 처리
date: 2023-03-27
published : true
categories: next.js session
---

## iron-session?
서명 및 암호화된 쿠키를 사용하여 데이터를 저장하는 Node.js의 stateless 세션 유틸리티. Next.js, Express 및 Node.js HTTP 서버에서 동작한다.
세션 데이터는 암호화된 쿠키(”seals”)에 저장된다. 그리고 사용중인 서버에서만 세션 데이터를 디코딩할 수 있다. iron session은 세션 ID가 없으므로 서버 관점에서 Iron 세션을 “무상태”로 만든다.
