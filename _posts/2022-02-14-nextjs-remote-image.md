---
layout: post
title: Next.js에서 외부 이미지 사용하기
description: 외부에서 가져온 이미지 Next.js Image 컴포넌트 최적화 적용하기
date: 2022-02-14
published : true
categories: next.js
---

Next.js는 `Image` 컴포넌트를 사용한 이미지 최적화를 지원한다. 이미지의 퀄리티는 유지하면서 용량을 줄이고 디바이스별 최적화를 하는 등 다양한 기능을 지원한다. 하지만 로컬이 아닌 외부에서 이미지를 가져와 사용하는 경우에는 악의적인 사용을 방지하기 위한 별도의 처리가 추가로 필요하다. `next.config.js`에서 `remotePatterns` 속성으로 옵션에 설정할 수 있다. 지정한 도메인에 있는 이미지만 가져와 Next.js의 이미지 최적화를 사용할 수 있게 해준다.  

```jsx
const nextConfig = {
  ***images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: '*.blankcdn.com',
      },
    ],
  },***
};

module.exports = nextConfig;
```

## 참고
https://nextjs.org/docs/api-reference/next/image#remote-patterns  


