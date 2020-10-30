---
layout: post
title: 'AWS CloudFront'
description: ''
date: 2020-10-28 18:06:00 +0530
categories: aws
---

`CloudFront`는 `AWS`에서 제공하는 `CDN`(컨텐츠 전송 네트워크)이다. `CDN` 서비스를 사용하면 서비스 대기 시간과 성능이 개선되고 이미지 등의 리소스에 접근하는 속도가 빨라진다. 서비스 지역이 `S3` 리전과 같은 지역이거나 가까우면 데이터 전송 속도가 빠르겠지만 다른 리전일 경우 다소 느릴 수 있다. `CloudFront`를 사용하면 이와 같은 문제를 개선할 수 있고 보안상으로도 SSL을 지원하기 때문에 안전하게 구성할 수 있다.  
`S3` 버킷에 리소스를 담고 `Route53`에서 해당 버킷으로 라우팅 처리할 수 있지만 `CloudFront`로 한번 더 감싼다고 이해할 수 있다.

## CloudFront와 S3를 함께 사용할 때 이점

- CDN을 통한 빠른 전송 속도
- S3에 직접 액세스 하는 것보다 싼 요금
- S3에 부하가 몰리지 않고 엣지 로케이션 캐싱되어 부하 분산
- 커스텀 도메인 사용 가능
- HTTPS 사용 가능

## CloudFront 적용하기

1. `Create Distribution` 선택
2. 필요한 항목들 입력하기
3. SSL 인증서 발급후 `CNAMEs` 부분과 `Custom SSL Certificate` 선택후 등록
4. `Default Root Object`에 `index.html` 입력하기

추가

`Vue`, `React` 와 같은 `SPA` 홈페에지의 경우 index.html 외에 다른 루트로 들어올 경우 403, 404와 같은 에러가 발생하기 때문에 `Error Pages`탭에서 추가 설정을 해준다.

Ex)

HTTP Error Code : 400: Bad Request

Error Caching Minimum TTL : 300

Customize Error Response : Yes

Response Page Path : /index.html

HTTP Response Code : 200: OK

위와 같은 식으로 에러를 뱉을때 index.html을 보여주면서 정상적인 데이터를 반환하는 처리를 해준다

400, 403, 404 정도
