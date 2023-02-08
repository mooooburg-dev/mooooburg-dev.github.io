---
layout: post
title: github page에 커스텀 도메인 연결하기
description: AWS Route53에서 github page 레코드 생성하기
date: 2020-11-03
categories: github
---

현재 블로그 `mooooburg-dev.github.io`에 `dev.drawyourmind.com` 도메인을 연결했다.
메인 도메인 `drawyourmind.com`은 aws에서 `Route53`을 이용해 관리중이라 Route53 내에서 `dev.drawyourmind.com` 레코드를 추가로 생성했다.

![image](https://user-images.githubusercontent.com/18201794/97936957-8fe4e080-1dc0-11eb-946f-1a2976ce1482.png)

Route53에서 `CNAME`을 `github.io`의 페이지 주소로 설정한다.

![image](https://user-images.githubusercontent.com/18201794/97937006-b99e0780-1dc0-11eb-97e1-190d2cab9c6f.png)

그리고 github 저장소 `Settings`에서 `Custom domain` 설정을 원하는 도메인으로 설정하면 된다.
레코드를 설정할 때 `CNAME`이 아닌 `A` 형식으로도 설정 할 수 있는데 [IP주소]로 설정이 가능하다.

- 192.30.252.153
- 192.30.252.154





