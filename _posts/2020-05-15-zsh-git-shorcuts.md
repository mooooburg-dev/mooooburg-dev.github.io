---
layout: post
title:  "oh-my-zsh 터미널에서 자주 사용하는 git 단축키 모음"
date:   2020-05-15 17:05:36 +0530
categories: git 
---
* gst - git status : 현재 local repository의 상태를 보여준다.

* gco - git checkout : 브랜치를 바꾸는 명령을 수행한다.

* ggl - git pull origin $(current_branch) : remote에서 현재 브랜치로 pull 명령을 수행한다.

* ggp - git push origin $(current_branch) : 현재 브랜치에서 remote로 push 한다.

* glg - git log --stat --max-count=10 : --stat : 각 커밋의 통계정보를 보여준다. git log + 상태정보를 보여준다.

* glgg - git log --graph--max-count=10 : --graph : 각 브랜치와 머지 히스토리 정보를 아스키 그래프로 보여준다. 현재 브랜치에 대한 정보를 보여준다.

* glgga - git log --graph--decorate--all : 위와 같으면 모든 브랜치에 대해 보여준다.

