---
layout: post
title:  "이클립스 Tomcat 실행 시 JDBC 관련 오류 해결"
description: "Web Deployment Assembly 확인하기"
date:   2020-05-17 21:57:36 +0530
categories: java
---
Build Path에 ojdbc 파일을 연결해 사용하다가 해당 프로젝트를 복사해서 새로운 프로젝트를 생성한뒤 톰캣을 실행하는 과정에서 dataSource와 관련된 에러를 뱉으면서 home에 접근하지 못하는 오류가 발생했다.


```xml
<!-- 에러가 발생하던 root-context.xml 부분 -->
<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
  <property name="driverClassName" value=""></property>
  <property name="jdbcUrl" value=""></property>
  <property name="username" value=""></property>
  <property name="password" value=""></property>
</bean>
```

위 부분과 관련되어 있는 부분까지 뒤졌지만 원인을 전혀 다른곳에 있었고 이클립스 IDE에서 해결했다.  
외부 라이브러리 파일을 추가할 때 Build Path에 추가하는 경우가 있는데
***Deployment Assembly > Web Deployment Assembly***에도 Source(jar)를 추가해줘야 했다.

![5F6F1B6B-1AF1-4B4B-A400-04538FB45A56](https://user-images.githubusercontent.com/18201794/82147903-f36b6800-988b-11ea-8b02-611fbd76a63e.png)

### 정리>
만일 테스트 환경에서는 정상적으로 동작하는데 Tomcat에서 JDBC 드라이버에 문제가 생겼다면 나온다면 Web Deployment Assembly를 확인해 봐야 한다.

