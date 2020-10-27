---
layout: post
title: 'file formdata 삭제하기'
description: '파일 업로드 처리중 formdata 비우기'
date: 2020-10-27 13:05:00 +0530
categories: javascript
---

파일 업로드 처리중에 아래와 같은 상황이 있었다. `upload file`을 이용해 업로드 할 파일을 선택후 X버튼으로 파일을 삭제하고 방금 선택헀던 같은 파일을 재선택할 경우 `change` 이벤트가 발생하지 않는다. `formdata`에 선택한 파일 정보가 남아있기 때문이다.

![image](https://user-images.githubusercontent.com/18201794/97255966-2f502380-1855-11eb-9a03-ece9a1c31b40.png)

```js
// js
document.querySelector('#qnaFile').val('');

// jquery
$('#qnaFile').val('');
```

위 코드로 formdata를 비울 수 있다.
