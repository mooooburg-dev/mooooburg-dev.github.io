---
layout: post
title:  "for in, for of 한줄 정리"
date:   2020-05-13 01:00:38 +0530
categories: javascript
---
ES6를 공부하면 접하게 되는 여러 가지 반복문의 형태들 중에 먼저 for~in과 for~of를 간단하게 정리한다면 아래 코드와 같다.

```javascript
let myString = "test";

for(let i in myString){
  console.log(i); // 0, 1, 2, 3 
}

for(let i of myString){
  console.log(i); // t, e, s, t
}
```

먼저 for~in의 경우 0, 1, 2, 3이 출력 되며 기본 for문과 같이 i는 인덱스를 반환한다. 반환되는 인덱스를 사용해 코드를 조작하는 방식이고, 
반면 for~of의 경우는 배열의 모든 원소를 돌며 원소가 가지는 값 자체를 반환한다. 인덱스가 필요한 상황이나 원소의 값이 필요한 상황에 따라서 for~in과 for~of 중 적절하다고 판단되는 형식을 사용하면 된다.


