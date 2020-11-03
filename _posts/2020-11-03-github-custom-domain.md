---
layout: post
title: 'github page에 custom domain 연결하기'
description: ''
date: 2020-11-03 10:30:00 +0530
categories: aws github domain
---

개인적으로 사용 중인 `mooooburg-dev.github.io` 개발 노트 블로그에 `dev.drawyourmind.com` 도메인을 연결했다.

`drawyourmind.com` 도메인은 AWS의 `Route53`으로 관리 중이라 `dev.drawyourmind.com` 레코드를 생성했다.

![github%20page%E1%84%8B%E1%85%A6%20custom%20domain%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20e059e9685a3549f9a62b682f09154231/Untitled.png](github%20page%E1%84%8B%E1%85%A6%20custom%20domain%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20e059e9685a3549f9a62b682f09154231/Untitled.png)

`Route53` 레코드 설정에서 `CNAME`을 `github.io`의 페이지 주소로 설정한다.

![github%20page%E1%84%8B%E1%85%A6%20custom%20domain%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20e059e9685a3549f9a62b682f09154231/Untitled%201.png](github%20page%E1%84%8B%E1%85%A6%20custom%20domain%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20e059e9685a3549f9a62b682f09154231/Untitled%201.png)

그리고 `github repository option` 화면에서 `Custom domain` 설정을 원하는 도메인으로 셋팅하면 끝!

`CNAME` 말고 `A` 형식으로 설정 할 수 있는데,

- 192.30.252.153
- 192.30.252.154

IP 주소로 설정이 가능하다.
