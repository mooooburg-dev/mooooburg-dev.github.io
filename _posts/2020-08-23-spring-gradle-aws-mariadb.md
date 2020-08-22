---
layout: post
title:  "Spring 환경에서 aws mariaDB 연결하기"
description: "mariaDB 연결 기본 정리"
date:   2020-08-23 09:00:00 +0530
categories: SpringBoot Gradle
---
> Spring gradle 환경에서 DB를 연결하는 방법은 여러가지가 있겠지만 Java나 Spring 학습단계에서 기본적으로 소개하는 방식이다. 데이터베이스의 정보(DB주소 및 계정정보)가 노출되는 방식이기 때문에 추가 작업이 필요하다.

1. build.gradle dependencies에 mariaDB JDBC를 등록하고
```java
> compile group: 'org.mariadb.jdbc', name: 'mariadb-java-client', version: '2.6.2'
```

2. application.properties 에다가 DB 정보를 넣어준다  
```properties
spring.datasource.hikari.driver-class-name=org.mariadb.jdbc.Driver
spring.datasource.hikari.jdbc-url=jdbc:mariadb://awsmariadb.cgacxljqur27.ap-northeast-2.rds.amazonaws.com:3306/[DB명]
spring.datasource.hikari.username=[DB계정]
spring.datasource.hikari.password=[DB비밀번호]
```