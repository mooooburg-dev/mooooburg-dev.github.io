---
layout: post
title: Next13 개발 환경 구성하기
description: tailwind, emotion, twin.macro, typescript로 구성한 프로젝트 준비하기
date: 2022-02-14
published : false
categories: next.js
---

SEO를 적용해야 하는 새로운 프로젝트를 시작하게 되면서 Next 13으로 프로젝트를 준비하게 됐고 기존부터 타입스크립트로 코드를 작성중이라 Next13 + TS 구성으로 프로젝트를 생성했다.
현재 사내에서 형제 프로젝트로 React Native 프로젝트가 진행중이라서 어떤식으로 조합이 이루어질지 몰라서 PC 및 모바일 웹 버전을 고려한 스타일링을 통일하여 tailwind를 선택했다. 기존에 사용중인 공통 컴포넌트가 emotion으로 작성되어 있어서 tailwind + emotion을 동시에 작성할 수 있는 twin.macro까지 적용해 보기로 했다.

1. setup
   ```bash
    yarn create next-app --typescript
   ```
2. tailwind Setup
   ```

   ```