---
layout: post
title:  "for in & for of 반복문 한줄 정리"
date:   2020-05-13 00:05:38 +0530
categories: Javascript  
---
ES6를 공부하면 접하게 되는 여러 가지 반복문의 형태들 중에 먼저 for in 과 for of 를 간단하게 정리한다면 아래 코드와 같다.

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
반면 for of의 경우는 해당 값 자체를 반환한다. 상황에 따라 for in과 for of 중에 더 적절하게 판단되는 형식을 사용하면 된다.


