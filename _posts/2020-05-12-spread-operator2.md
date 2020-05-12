---
layout: post
title:  "push() 메서드 대신 펼침 연산자로 원본의 변경을 피하라"
date:   2020-05-12 23:39:38 +0530
categories: Javascript ES6 
---

```javascript
function addFreeGift(cart) {
    if (cart.length > 2) {
        // cart.push(reward); // 원본이 조작되는 오류가 발생한다    
        // return cart;

        return [...cart, reward];
    }
    return cart;
}
```

배열의 push() 메서드의 경우 원본이 변경 되는 점을 유의해야 한다. 이러한 상황에서 펼침 메서드를 활용해서 배열을 추가할 수 있다. 위 코드와 같이 cart 배열에 reward를 추가한다고 할 때,

```javascript
return cart.push(reward);
```

cart 배열 자체가 변경되며,

```javascript
return [...cart, reward];
```

하게 되면 cart 배열이 아닌 새로운 배열이 반환된다.