---
layout: post
title: CursorAI 활용 가이드 - 사이드 프로젝트를 빠르게 완성하는 3단계
description: CursorAI와 LLM을 활용해 사이드 프로젝트를 빠르고 효율적으로 완성하는 3단계 가이드
date: 2025-01-24
published: true
categories: IDE AI
---

Microsoft의 엔지니어 [**Zohaib Rauf**](https://www.linkedin.com/in/zohaibrauf/)는 CursorAI와 LLM을 활용해 그동안 미뤄왔던 다양한 사이드 프로젝트를 빠르게 제작했다고 합니다. 오늘은 그가 추천한 방법을 바탕으로 CursorAI를 효과적으로 활용하는 3단계를 소개해 드리겠습니다.

## 1단계: **스펙 구상하기**

먼저 **GPT**를 활용해 애플리케이션의 스펙을 구체화하세요. 명확하고 구체적인 기술 명세서를 작성하면 프로젝트 진행이 훨씬 수월해집니다.  
이때 다음과 같은 요청을 GPT에 활용할 수 있습니다:

> "다른 사람이나 AI가 이 문서를 보고 웹사이트를 만들 수 있도록 markdown 형식의 명세서를 만들어줘. 프로젝트 세부사항, UX/UI, 각 기능에 필요한 것들을 반드시 포함해야 해. 기술은 TypeScript, React, TailwindCSS 위주로 사용할 거야."

**TIP:**

- 작성된 스펙은 반드시 별도로 저장해 **SPEC.md** 파일로 관리하세요.
- 나중에 이 문서를 참조하면서 프로젝트를 체계적으로 진행할 수 있습니다.

## 2단계: **초기 코드 생성하기**

Vite 등으로 프로젝트를 시작한 후, **SPEC.md 파일**을 프로젝트 폴더에 추가하세요.  
Cursor IDE에서 다음과 같은 단계를 따라 초기 코드를 생성할 수 있습니다:

1. **Cursor IDE** > Composer > Select Agent로 이동
2. SPEC.md를 컨텍스트로 추가
3. 구현 요청

몇 분 안에 기본적인 뼈대가 완성되며, 초기 코드 작성 시간을 크게 단축할 수 있습니다.

## 3단계: **작은 단위로 기능 쪼개기**

세부 기능을 구현할 때는 **작은 단위로 나누어 요청**하는 것이 중요합니다.

> 큰 단위로 요청하면 오류가 발생할 가능성이 높고, 수정하는 데 더 많은 시간이 소요됩니다.

- 기능별로 작업을 나누어 요청하세요.
- 기존 코드나 문서 링크를 적극 활용해 컨텍스트로 제공하세요.
- 이렇게 하면 AI의 환각(hallucination)을 방지하고 정확도를 높일 수 있습니다.

---

## CursorAI 활용 꿀팁

### 1. LLM 혼합 사용

Zohaib는 기능 초안을 작성할 때 **o1**을, 반복 작업은 **Claude-3.5-sonnet**을 활용한다고 합니다. 여러분도 프로젝트 성격에 맞게 다양한 LLM을 활용해 보세요.

### 2. v0.dev로 UX 쉽게 구현

v0.dev 같은 툴을 사용하면 UX/UI 작업 시간을 줄이고 효율성을 극대화할 수 있습니다.

![v0.dev screenshot](https://vercel.com/_next/image?url=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Fcontentful%2Fimage%2Fe5382hct74si%2F3CSHPVw6n6ZPBWXZfFycpp%2Fb499dbf7977ad404be660a892da2100a%2F600x300.png&w=1920&q=75)

### 3. 프로젝트 디렉토리 관리

- **SPEC.md**: 프로젝트 관련 내용을 체계적으로 관리
- **.cursorrules** 파일: 프로젝트에서 사용할 기술 스택을 지정하거나 제외할 기술을 명시

---

## CursorAI로 프로젝트를 빠르게 완성하세요

CursorAI와 LLM을 활용하면 프로젝트 진행 속도가 빨라지고 효율성이 높아집니다. 그러나 AI가 작성한 코드를 제대로 이해하지 못하면 디버깅에 어려움을 겪을 수 있으니, **코드를 파악하며 작업을 진행하는 것**도 잊지 마세요.
