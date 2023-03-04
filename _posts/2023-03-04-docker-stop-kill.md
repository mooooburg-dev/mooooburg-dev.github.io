---
layout: post
title: docker stop, kill 커맨드 차이점
description: 
date: 2023-03-04
published : true
categories: docker
---

![image](https://user-images.githubusercontent.com/18201794/222878453-b7bf2795-5f77-4fe5-bac9-c7c9095682d4.png)

우선 stop, kill 두 명령어 모두 실행 중인 컨테이너를 종료할 때 사용하는 명령어이다.

차이점은 stop은 진행 중이던 작업을 완료하고 종료시키기에 약간의 딜레이 시간이 있고

kill은 진행 중인 작업과 상관없이 즉시 종료 하기 때문에 딜레이 시간이 없다.


