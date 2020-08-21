---
layout: post
title:  "SpringBoot Gradle 프로젝트에서 war 빌드시 톰캣에 정상 배포 실패 현상"
description: "SpringBoot의 내장 톰캣을 만나다"
date:   2020-08-21 00:00:00 +0530
categories: SpringBoot, Gradle
---
기존 maven 프로젝트로 진행한 war 파일을 톰캣에 배포 하는 경우, 외장 톰캣의 기본 패스인 webapps를 통해 문제 없이 프로젝트를 실행시켰다.
하지만 해당 프로젝트를 SpringBoot Gradle 방식으로 변경하고 비슷한 방법으로 war 파일 빌드 후 같은 방식으로 톰캣에 올렸는데 404에러가 발생했다.  
단순 path문제 또는 그 이상의 문제일 것을 예상하고 여러가지 방식을(삽질을) 시도하다가 아래 포스팅들까지 적용해 봤지만 마찬가지였다.

**gradle build을 이용한 war 배포 관련 포스팅**  
  - https://gigas-blog.tistory.com/115{: target="_blank"}
  - https://cpdev.tistory.com/46{: target="_blank"}

위의 포스팅 내용을 보면 메인 jar와 war 빌드시에 메인 클래스를 실행하는 방식이 다르다는 이야기인데 왠지 그럴듯 하여 적용해봤지만 같은 문제가 발생하였다.  
추가 테스트를 진행하던 중에 이상한 점을 발견했는데 SpringBoot 프로젝트 생성시 여러 의존성을 선택 주입하는데 이 부분에서 만약 아무것도 선택하지 않은 플레인 상태에서 war 빌드만 진행하고 톰캣에 올렸을 경우는 404가 발생하지 않고 정상 배포가 되었다.  
그렇다면 의존성이 주입되는 과정에서 어떤 환경이 변한다는 얘기가 되는데, 하나하나 테스트를 하다보니 눈에 띄는 두가지가 있었다.

  - implementation 'org.springframework.boot:spring-boot-starter-jdbc'  
  - implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:2.1.3'


진행하고 있는 프로젝트의 경우는 위 두가지를 제외하면 정상 작동할 것으로 예상됐지만 제외하고 빌드할 경우 에러가 발생해서 눈으로 테스트 해보지는 못했다.  
위 부분에 대해 다양한 방법을  시도하다가 결국 내장 톰캣을 테스트 해봤다. 내장 톰캣의 경우 컴파일된 파일을 실행만 하면 톰캣이 실행되는데 이 경우 위의 삽질이 무색할 정도로 너무 깔끔하게 정상 작동하였다.

**[REST API 실습] 4. Springboot 프로젝트 AWS EC2 인스턴스에 배포**  
https://wickies.tistory.com/102{: target="_blank"}  

스프링부트 jar 실행하기 (Run spring boot runnable jar)  
https://navy-apple.com/dev/spring/boot-runnable-jar{: target="_blank"}  



