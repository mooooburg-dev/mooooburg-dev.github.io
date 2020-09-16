---
layout: post
title:  "ssh 접속 오류 REMOTE HOST IDENTIFICATION HAS CHANGED"
description: "ssh-keygen으로 해결"
date:   2020-09-15 09:00:00 +0530
categories: ssh
---

$$$ ssh -i pem파일경로 ec2-user@IP주소 $$ 
위 코드로 aws의 ec2로 접속을 하려고 했다. 오래전도 아니고 불과 며칠전에 잘 접속했었던 방법이다.  
그렇지만 나를 맞이한 건 WARNING 코드

```bash
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

발생된 SSH 접속 오류는 IP는 동일하지만 목적지 서버 장비가 바뀌었다거나 VMware와 같은 가상 컴퓨터의 IP는 동일하지만 실질적인(물리적) 서버가 바뀌었을 경우 나오는 일종의 경고성 알림이다.

$$$ ssh-keygen -R 대상IP주소 $$