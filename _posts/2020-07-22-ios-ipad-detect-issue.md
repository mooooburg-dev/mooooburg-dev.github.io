---
layout: post
title:  "iPad 분기 처리 이슈"
description: "iPad의 userAgent가 macOS로 나온다고??"
date:   2020-07-22 00:00:00 +0530
categories: Javascript 
---

Back-end에서 동적 생성된 blob type의 pdf 파일을 `<object>`태그로 embed 하여 화면 표시 및 프린트 기능을 지원하고 있다.  
브라우저는 chrome과 safari를 지원하고 있고, tablet(ipad, galaxy tab)을 지원한다.

![image](https://user-images.githubusercontent.com/18201794/88029065-7652bc80-cb74-11ea-9e8f-0797ee1bdf7a.png)

Invocie 버튼을 클릭해 모달을 띄우고 페이지내에 pdf를 심으려고 했다.

관련 링크  
<https://github.com/mooooburg-dev/medit-partner-portal/issues/1>{: target="_blank"}

#### 이슈1>  
ipad chrome/safari에서 pdf가 표시되지 않는다.  
(iframe, embed, obejct 태그중에 object 태그만이 mac safari에서 표시가 되어 object 태그로 사용하였고, 나머지 태그 역시 테스트 하였지만 세가지 형식 모두 표시가 되지 않았다)

#### 해결1>  
iPad 일때는 팝업을 띄우자.  
"왠만하면 브라우저별로 기능을 넣고 빼고 하고 싶지 않았지만 쩝..."

#### 실행1>  
간단하게 생각하고 device detect 검색으로 찾은 플러그인을 적용했다.
ex) vue-detect-device, vue-ios-decect와 같은 것들..

#### 이슈2>  
플러그인에서 사용하는 navigator.userAgent가 ipad를 mac os로 리턴하는 문제가 있었다.  
chrome 개발자도구에서 ipad로 설정 후 테스트 했을때는 문제가 없었지만 실제 ipad safari로 띄워놓고 보면 문제가 발생하다.  
우선 사용한 플러그인이 문제일 것이라 생각하고 다른 플러그인을 설치해 사용해 보았으나 하나같이 safari 에서 ipad를 ipad라 인식하지 않았다.  

navigator.userAgent → ***Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_3) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.5 Safari/605.1.15***

userAgent의 문자열에서 'ipad'를 찾으려고 했는데 문자조합에서 ipad가 포함되어 있지 않았고 mac safari와 비교했을때 99% 같은 문자열을 반환하고 있었다.
ipad safarai가 mac safari와 같은 userAgent를 리턴하면서 mac과 ipad가 같은 놈처럼 굴었다.

#### 해결2>  
한 블로그에서 userAgent의 문자열을 가지고 분기 처리를 해놓은 해결책을 찾았다.  

**iPad**
```js
const ua = window.navigator.userAgent.toLowerCase();
const isiPad = ua.indexOf('ipad') > -1 || ua.indexOf('macintosh') > -1 && 'ontouchend' in document;
```
**iPhone**
```js
const ua = window.navigator.userAgent.toLowerCase();
const isiOS = ua.indexOf('iphone') > -1 || ua.indexOf('ipad') > -1 || ua.indexOf('macintosh') > -1 && 'ontouchend' in document;
```
**macOS**
```js
const ua = window.navigator.userAgent.toLowerCase();
const isMac = ua.indexOf('macintosh') > -1 && !('ontouchend' in document);
```

![image](https://user-images.githubusercontent.com/18201794/88029065-7652bc80-cb74-11ea-9e8f-0797ee1bdf7a.png)

#### 정리>
어떤 이유에서인지 ipad의 userAgent에 ipad 문자열이 포함되지 않는다. 결국 문자열로 분기처리를 해야하는데 찝찝한 부분으로 남지만 오늘도 역시나 바쁜 일정이니까 노트에 기록하는 것으로 아쉬움을 달랜다.