---
layout: post
title: 'Linux java -jar 백그라운드에서 실행(nohup)'
description: 'java를 백그라운드에서 실행하기'
date: 2020-09-22 15:15:00 +0530
categories: java
---

1. 리눅스 환경에서 Java(jar)를 데몬처럼 실행

```bash
$ java -jar [파일명] &

#사용자가 로그아웃 하거나 터미널을 종료할 경우 프로그램이 종료됨
```

2. 사용자가 로그아웃해도 백그라운드에서 실행되는 명령어

```bash
$ nohup java -jar [파일명] &
```

3. 프로세스 종료

```bash
# 찾기
$ ps -ef|grep '[파일명]'

# 종료
$ kill -9 [pid번호]
```
