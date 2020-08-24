---
layout: post
title:  "터미널에서 graldew 빌드시 command not found, permission denined 뜰때"
description: "gradlew에 권한 부여하면 끝"
date:   2020-08-24 09:00:00 +0530
categories: gradle gradlew build
---
터미널에서 스프링 빌드 하는 상황에서 퍼미션이나 파일을 찾을 수 없다는 에러가 나올때 권한 문제일 가능성이 크다.  
sudo 붙여서 해결 안되고 chmod 권한 조정으로 해결.

> chmod +x gradlew

