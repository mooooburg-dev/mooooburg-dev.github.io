---
layout: post
title: 'github page에 custom domain 연결'
description: ''
date: 2020-11-03 10:30:00 +0530
categories: aws github domain
---

현재 이 블로그 `mooooburg-dev.github.io`에다가 `dev.drawyourmind.com` 도메인을 연결했다.

개인적으로 20년 가까이 사용중인 `drawyourmind.com`은 AWS의 `Route53`으로 관리중이라 AWS에서 `dev.drawyourmind.com` 레코드를 생성했다.

![image](https://user-images.githubusercontent.com/18201794/97936957-8fe4e080-1dc0-11eb-946f-1a2976ce1482.png)

별다른 설정은 따로 없고 `Route53`에서 `CNAME`을 `github.io`의 페이지 주소로 설정한다.

![image](https://user-images.githubusercontent.com/18201794/97937006-b99e0780-1dc0-11eb-97e1-190d2cab9c6f.png)

그리고 `github repository`페이지의 `Setting` 화면에서 `Custom domain` 설정을 원하는 도메인으로 셋팅하면 끝.

레코드를 설정할 때 `CNAME`이 아닌 `A` 형식으로도 설정 할 수 있는데,

- 192.30.252.153
- 192.30.252.154

IP 주소로 설정이 가능하다.

![image](https://p.kindpng.com/picc/s/128-1280187_github-logo-png-github-transparent-png.png)
