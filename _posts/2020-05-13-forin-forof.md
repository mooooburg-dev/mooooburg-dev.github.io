---
layout: post
title:  "for in & for of 반복문 한줄 정리"
date:   2020-05-13 00:05:38 +0530
categories: Javascript  
---
for in 과 for of 를 간단하게 정리한다면,

```javascript
let myString = "test";

for(let i in myString){
  console.log(i); // 0, 1, 2, 3 
}

for(let i of myString){
  console.log(i); // t, e, s, t
}
```

for in의 경우 0, 1, 2, 3이 출력되며 기본 for문과 같이 i는 인덱스를 반환한다.
반면 for of의 경우는 해당 값 자체를 반환한다.


