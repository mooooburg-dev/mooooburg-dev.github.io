---
layout: post
title:  "DOM에 접근해야 하는 시점이 애매할 때 $nextTick 사용하기"
description: "화면에는 있는데 찾을 수 없는 요소라고 콘솔에 에러가 뜰 때"
date:   2020-08-07 00:00:00 +0530
categories: vue
---
Vue로 개발을 진행하다면 보면 기존과 약간 다른 개발 방식에 애매한 상황이 생기는데 그중 하나로 Vue의 데이터와 화면의 UI를 찾아 접근해야 하는 상황에서 DOM을 찾지 못하는 상황이 있다.  

데이터를 통해서 만들어지게 되는 DOM이 완성되기 이전 시점에 호출을 하려고 하는 상황인데, 어떠한 데이터를 변수에 담아 화면이 갱신되는 DOM에 바로 접근하려고 하면 DOM 요소가 없다는 에러를 뱉는다.  

모든 데이터 처리가 비동기로 처리되는 자바스크립트 특성 때문에 DOM이 갱신되기 전 탐색하는 상황에서 생기는 현상이다. 그래서 옛날 방식 setTimeout을 이용해 약간의 시간차를 주게 되면 문제없이 DOM에 접근할 수 있게 된다.

개발자 관점에서 setTimeout의 활용이 받아들여지는 부분이 있고 그렇지 않은 부분이 있다. 확실히 시간적 딜레이를 주어야 하는 상황에서 setTimeout의 활용은 어떨지 모르겠지만 위와 같은 상황에 0.5초의 갭 때문에 활용하는 setTimeout은 적절하지 않다. 그럴 때 사용할 수 있는 callback 함수가 **$nextTick**이다.

```js
created: function(){
  // ...

  this.$nextTick(() => {
    let dom = document.getElementById('item');
    dom.style.backgroundColor = 'orange';
  })
}
```

코드를 $nextTick으로 감싼뒤 callback을 통해 DOM에 접근한다. 그렇게 되면 Vue.js에서 데이터를 갱신하고 **화면UI 렌더링까지 완료된 후 nextTick의 콜백이 실행되고 DOM으로 접근**하는 과정을 거치게 된다.

[$nextTick](https://kr.vuejs.org/v2/api/index.html#Vue-nextTick){: target="_blank"}

