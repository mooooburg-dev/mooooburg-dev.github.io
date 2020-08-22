---
layout: post
title:  "Spring gradle 환경에서 aws mariaDB 연결(기본)"
description: "mariaDB 연결 기본 정리"
date:   2020-08-23 09:00:00 +0530
categories: SpringBoot Gradle
---
> Spring gradle 환경에서 aws mariaDB 연결하는 방법

1. build.gradle dependencies에 mariaDB JDBC를 등록하고
```java
> compile group: 'org.mariadb.jdbc', name: 'mariadb-java-client', version: '2.6.2'
```

2. application.properties 에다가 DB 정보를 넣어준다  
```properties
spring.datasource.hikari.driver-class-name=org.mariadb.jdbc.Driver
spring.datasource.hikari.jdbc-url=jdbc:mariadb://awsmariadb.cgacxljqur27.ap-northeast-2.rds.amazonaws.com:3306/[DB명]
spring.datasource.hikari.username=admin
spring.datasource.hikari.password=^pass0912_
spring.datasource.hikari.connection-test-query=SELECT 1
```