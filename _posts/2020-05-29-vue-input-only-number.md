---
layout: post
title:  "Vue.js | v-int 활용하기 int와 float만 허용한다"
description: ""
date:   2020-05-29 19:27:36 +0530
categories: Vue Javascript 
---
input 텍스트 필드에 숫자만 입력해야하는 경우 사용한다.  
https://www.npmjs.com/package/vue-input-only-number 


```javascript
import onlyInt, { onlyFloat } from 'vue-input-only-number';

Vue.use(onlyInt);
Vue.use(onlyFloat);

<input type="text" v-int>
<input type="text" v-float>
```

현재 버전에는 천 단위 콤마와 같은 기능은 따로 없다.


