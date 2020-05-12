---
layout: post
title:  "펼침 연산자로 배열을 본떠라"
date:   2020-05-12 13:03:38 +0530
categories: Javascript ES6 
---

```javascript
function removeItem(items, removable) {
    const index = items.indexOf(removable);
    return [...items.slice(0, index), ...items.slice(index + 1)];
}

const books = ["practical vim", "moby dick", "the dar tower"];
const recent = removeItem(books, "moby dick");
const novels = removeItem(books, "practical vim");
console.log(recent);
console.log(novels);
```


펼침 연산자를 slice() 메서드와 함께 사용하면 하위 배열을 목록으로 변환해 대괄호 안에 작성할 수 있다. 실제로 배열처럼 보이는 효과도 있다. 더 중요한 점은 원래 배열에 영향을 주지 않고 새로운 배열을 생성해준다는 점이다.


```javascript
const book = ["Reasons and Persons", "Derek Parfit", 19.99];
function formatBook(title, author, price) {
    return `${title} by ${author} $${price}`;
}

// console.log(formatBook(book[0], book[1], book[2]));
console.log(formatBook(...book)); // Reasons and Persons by Derek Parfit $19.99
```

매개변수의 양이 바뀌었을 때도 코드를 고치지 않아도 된다.


