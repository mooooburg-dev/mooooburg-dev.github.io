---
layout: post
title: '터미널 find 커맨드로 파일 검색하기'
description: '자주 사용하는 find 커맨드 정리'
date: 2020-09-17 10:14:00 +0530
categories: cli
---

맥 터미널(unix) 환경에서 find 커맨드를 활용하여 파일을 검색하는 방법이다. GUI 환경에서 스팟라이트나 파인더를 이용하여 파일을 검색하는 방법이 있다면, 마찬가지로 쉘 환경에서도 파일을 검색하는 방법들이 다양하게 존재한다.

- locate : 미리 빌드된 데이터베이스에서 빠르게 검색
- grep : 파일 내의 문장들에서 문자열 패턴을 검색
- mdfind : 파일의 메타데이터를 검색

# find 커맨드의 기본 내용

find 등의 커맨드를 사용하면 GUI 환경에서 꼼수로 숨겨둔 파일은 식은 죽 먹기로 찾을 수 있다. 한번 익혀두면 잘 잊어버리지 않으니 초기에 잘 기억하여 활용하자.

**기본 문법**

```bash
$ find [경로] [플래그] [표현식]
```

- 경로 : /, ~, ~/Desktop 등의 경로 입력
- 플래그 : -name 등의 플래그(옵션) 입력
- 표현식 : 검색할 파일의 이름 혹은 패턴 등의 표현식을 입력

### 몇가지 예시

- 현재 디렉토리(.) 내 '.txt'를 포함한 모든(\*) 파일 검색

```bash
$ find . -name "*.txt"
```

- root 디렉토리(/) 내 '.txt'를 포함한 모든(\*) 파일 검색

```bash
$ find / -name "*.txt"
```

# find 커맨드 활용

find 커맨드를 활용하는 몇가지 예시이다. 각각의 커맨드에 대한 자세한 설명은 생략한다.

### 결과물을 카운팅해서 숫자로만 보기

결과물을 일일이 출력하지 않고 카운팅한 결과만 보는 방법이다. 파이프 옵션과 함께 'wc -l(소문자 L)'을 사용하면 된다.

```bash
$ find . -name "*.txt" | wc -l
```

- wc : word count의 줄임말

### 파일 타입으로 구분하여 검색하기

-type 옵션을 통해 파일 타입을 d(directory) 혹은 f(file)로 구분하여 검색이 가능하다

**파일만 검색**

```bash
$ find . -name "exam*" -type f
./example1.txt
./example2.txt
./example3.txt
```

**디렉토리만 검색**

```bash
$ find . -name "exam*" -type d
./example
```

**파일 및 디텍토리 모두 검색**

```bash
# 옵션을 따로 추가하지 않음
$ find . -name "exam*"
./example
./example1.txt
./example2.txt
./example3.txt
```

### -not 옵션을 통해 반전

위 내용들에 -not만 추가하면 결과물이 반전된다.

```bash
# 현재 디렉토리 내으 파일들 중 이름 시작에 ex를 포함하지 않는 모들 파일 찾기
$ find . -not -name "ex*"

```

**참고 링크**

[[맥 터미널 / Unix] find 커맨드로 파일 검색하기 - Mac In June](https://macinjune.com/all-posts/mac/terminal/%EB%A7%A5-%ED%84%B0%EB%AF%B8%EB%84%90-unix-find-command%EB%A1%9C-%ED%8C%8C%EC%9D%BC-%EA%B2%80%EC%83%89%ED%95%98%EA%B8%B0/)
