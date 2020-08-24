---
layout: post
title:  "터미널에서 graldew 빌드시 command not found, permission denined 뜰때"
description: "gradlew에 권한 부여하면 끝"
date:   2020-08-24 09:00:00 +0530
categories: gradle gradlew build
---
터미널에서 스프링 빌드 하는 상황에서 퍼미션이나 파일을 찾을 수 없다는 에러가 나올때 권한 문제일 가능성이 크다.  
권한 문제이니 sudo로 해결해보려고 했는데 비슷한 결과가 나왔고 chmod으로 권한 조정해서 해결하였다.

```
> chmod +x gradlew
```

