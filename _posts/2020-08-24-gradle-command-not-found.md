---
layout: post
title:  "터미널에서 gradlew 빌드시 command not found, permission denined 뜰때 권한 조정하기"
description: "gradlew에 권한 부여하면 끝"
date:   2020-08-24 09:00:00 +0530
categories: gradle gradlew build
---
운영 서버 환경 셋팅하면서 테스트용으로 배포 파일을 빌드하여 올려보려고 했다.  
이클립스에서 tasks로 clean, build를 돌렸는데 에러가 나서 터미널 명령어로 빌드를 시도해보려 했는데 빌드 상황에서 퍼미션이나 파일을 찾을 수 없다는 에러가 나왔다.  
gradle은 당연히 설치되어 있는 상태였고 환경변수 탓인가 의심했는데 퍼미션 문제라고 하니 sudo로 해결하려고 했는데 되지 않았고 chmod로 권한 조정하고 해결했다.

```
> chmod +x gradlew
```

