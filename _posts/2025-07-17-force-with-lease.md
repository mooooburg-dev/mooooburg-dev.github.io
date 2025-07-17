---
layout: post
title: 협업 중 안전하게 force push 하기
description: 강제 푸시가 필요한 상황에서 실수 없이 안전하게 사용하는 방법
date: 2025-07-17
published: true
categories: git
---

로컬에서 커밋 스쿼시나 rebase 한 다음 푸시하려다 보니 force 옵션 쓸 일이 생김.  
근데 그냥 --force 쓰면 협업 중에 위험할 수 있음.  
다른 사람이 올린 커밋을 모르게 날려버릴 수도 있음.

그럴 때는 `--force-with-lease` 옵션 사용하는 게 훨씬 안전함.

```
git push --force-with-lease origin master
```

이 명령어는,

- “원격 브랜치 상태가 내가 마지막으로 본 상태랑 동일할 때만 푸시 허용”
- 조건이 붙어 있어서 누군가 먼저 커밋 올렸으면 푸시가 거부됨.
- 실수 방지용 안전장치라고 보면 됨.

⸻

force push 관련 명령어 정리

**명령어 설명**

- `git push --force origin master` 무조건 강제 푸시. 위험함.
- `git push --force-with-lease origin master` 안전한 강제 푸시. 협업 시 권장.
- `git push -f origin master` --force 축약형. 위험도 동일함.

혼자 작업 중이면 상관 없지만, 협업 중이면 --force-with-lease 쓰는 게 맞음.  
습관처럼 써두는 게 좋음.
