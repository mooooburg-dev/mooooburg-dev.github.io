---
layout: post
title: 'ssh 접속 오류 REMOTE HOST IDENTIFICATION HAS CHANGED'
description: 'ssh-keygen으로 해결'
date: 2020-09-15 09:00:00 +0530
categories: ssh
---

회사 [프로젝트](https://github.com/mooooburg-dev/medit-partner-portal)의 기획자 이슈 요청을 처리하기 위해 터미널을 활용하여 aws의 ec2에 접속하려 했다. 오래전도 아니고 불과 며칠전에 잘 접속했었던 방법이다.

```
$ ssh -i pem파일경로 ec2-user@IP주소
```

그렇지만 나를 맞이한 건 WARNING 코드, REMOTE HOST IDENTIFICATION HAS CHANGED!

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!

Someone could be eavesdropping on you right now (man-in-the-middle attack)!

It is also possible that a host key has just been changed.

The fingerprint for the RSA key sent by the remote host is

7a:1a:88:.......(생략)

Please contact your system administrator.

Add correct host key in /root/.ssh/known_hosts to get rid of this message.

Offending RSA key in /root/.ssh/known_hosts:12

RSA host key for 192.168.0.2 has changed and you have requested strict checking.

Host key verification failed.
```

> 원격 호스트 정보가 변경 되었고 기존에 등록되어있던 RSA Key가 다르다.  
> 누군가 기존 접속 정보를 바꾸어 정보를 가로채는 man-in-the-middle attack 발생에 유의하라.  
> 해당 경고를 제거하려면 /root/.ssh/known_hosts 올바른 Host Key를 추가해라.

대략 위의 내용으로, 발생된 SSH 접속 오류는 IP는 동일하지만 목적지 서버 장비가 바뀌었다거나 VMware와 같은 가상 컴퓨터의 IP는 동일하지만 실질적인(물리적) 서버가 바뀌었을 경우 나오는 일종의 경고성 알림이다.

```
$ ssh-keygen -R 대상IP주소
```

위 명령어를 사용해 known_hosts 정보를 업데이트 하여 문제를 해결할 수 있다.
