---
layout: post
title: Vue에서 자체 페칭을 이용한 동적 Markdown 데이터 렌더링 하기
description: vue-markdown과 copy-webpack-plugin을 활용한 자체 데이터 페칭과 동적 마크다운 렌더링
date: 2022-02-09
published : true
categories: vue markdown
---

개인 포트폴리오 사이트에서 Works 내 작업물 컨텐츠를 일반 HTML 기반의 개별 컴포넌트 형태로 가지고 있다보니 운영 비용이 크고 코드의 양 또한 많아져서 리소스 낭비가 컸다. 무엇보다 하드 코딩 형태의 정적 파일이 비효율적이고 개선이 여지가 많아 보였다. 작업물을 추가할 때 마다 불편했다. 제작 당시 시간 없다는 핑계로 막 잡은 ul, li, br 태그로 난무한 페이지를 더 이상 지켜 보고만 있을 수는 없었다.

## 개선사항
router에서 일일히 import 했었던 컨텐츠 컴포넌트를 제거하고 WorkContainer 컴포넌트 한 개만 import 한다. Markdown 데이터를 활용해서 동적으로 화면을 그려 운영 리소스를 줄일 수 있도록 개선한다.

## 이슈
파일이나 폴더를 읽을 수 있는 fs 모듈을 사용하려고 했다. 그런데 Node 영역에서 사용할 수 있는 fs모듈은 브라우저 클라이언트 영역에서는 사용 할 수 없고 폴더에 접근조차 할 수 없었다.

## 해결
markdown 파일을 빌드 묶음에 포함해서 런타임 시점에 자체적으로 페칭할 수 있는 구조로 변경했다. 빌드 시에 생성되는 `dist` 폴더에 웹팩 플러그인 중 파일을 빌드 묶음에 복사할 수 있는 `copy-webpack-plugin`을 사용했다. 플러그인은 설치 후 `vue.config.js`에 적용하였다. 자체 페칭을 통해서 Markdown 데이터를 동적으로 가져오고 [`vue-markdown`](https://www.npmjs.com/package/vue-markdown) 라이브러리를 사용해서 WorkContainer 안에서 화면을 그려준다.

```jsx
***const CopyPlugin = require('copy-webpack-plugin')***

module.exports = {
  lintOnSave: true,
  configureWebpack: {
    ***plugins: [
      new CopyPlugin({
        patterns: [{ from: 'src/posts', to: 'static/posts' }],
      }),
    ],***
    ...
  },
}
```

![image](https://user-images.githubusercontent.com/18201794/217805029-b4595ed1-de8a-41b6-8c52-692cde64e47f.png)

`src/posts` 폴더에 있는 파일들을 dist 폴더 내 `static/posts` 폴더에 복사하도록 설정했다. 이미지처럼 dist/static 폴더 하위에 posts 폴더와 md 파일들이 같이 포함되어 빌드 된다.

```jsx
const works = [
  'hsmoa-backoffice',
  'medit-partner-portal',
  'hr',
  'adidas-golf',
  'dior-gallery',
  'ybm-digital-book',
  'sns-marketing',
  'vual',
  'meritz-direct',
  'gooutstore',
  'lotte-howmuch',
  'all',
]

...

{
  path: '/works',
  name: 'works',
  component: WorksView,
  **children: works.map((route) => ({
    path: route,
  })),**
},
```

`router` 데이터에서 works 내 children 속성에 각 작업물의 path를 배열 형태로 설정해 주었다. 이 path는 md 파일명과 동일하도록 설정하고 데이터를 자체적으로 페칭할 때 url로 사용한다.

```jsx
**<work-container :markdown="arrPathName[pageNum - 1]"></work-container>**
```

`WorkView` 컴포넌트에서는 하위 컴포넌트인 `WorkContainer`에 `path` 명만 전달한다. pagination 처리는 기존과 동일하게 사용하고 `page`가 바뀔 때 마다 markdown path 데이가 바뀌고 `watch` 구문에서 `getData` 메서드를 호출하게 된다.

```jsx
**<vue-markdown v-if="md !== null" :source="md" />**
...
watch: {
  markdown: {
    handler() {
      this.getData()
    },
    immediate: true,
  },
},
```

`vue-markdown` 라이브러리 컴포넌트에 페칭한 데이터를 전달해서 새로운 화면을 그리도록 처리했다.