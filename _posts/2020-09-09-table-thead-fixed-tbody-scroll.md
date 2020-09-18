---
layout: post
title: 'table의 thead 고정과 tbody 스크롤'
description: '골치아픈 테이블 스크롤 박제'
date: 2020-09-09 10:14:00 +0530
categories: CSS
---

진행중인 프로젝트가 유난히 테이블과의 싸움이다. 그 중 하나가 헤더 고정 이슈인데 `<tr>`이 한개가 아니고 `<colspan>`, `<rowspan>`으로 셀이 합쳐지면서 헤더가 고정이 되는 부분들이 있다보니 은근히 노가다 이슈가 있다.

![image](https://user-images.githubusercontent.com/18201794/93560036-19c91d80-f9bc-11ea-85e4-497f302617da.png)

위 그림의 table은
.table-wrapper > .result-table > .sticky-th, .stickty-th-two와 같은 구조를 가지고 있고 코드는 아래와 같다.
특정 프로젝트에 실제 사용된 코드이다보니 다른 프로젝트에 적용하려면 필수 커스터마이징이 필요하고 코드는 개인적인 참고용으로 작성하였다.

**HTML**

```html
<div class="table-wrapper">
  <table width="100%" class="contentTable table-bordered result-table" style="max-height:36px;">
    <colgroup>
      <col width="8%" />
      <col width="27%" />
      <col width="13%" />
      <col width="13%" />
      <col width="13%" />
      <col width="13%" />
      <col width="13%" />
    </colgroup>
    <thead>
      <tr>
        <th class="text-center fixedHeader sticky-th" rowspan="2">No</th>
        <th class="text-center fixedHeader sticky-th" rowspan="2">{{ $t('pm.ability.name') }}</th>
        <th class="text-center fixedHeader sticky-th" colspan="2">{{ $t('pm.final.finResult') }}</th>
        <th class="text-center fixedHeader sticky-th" colspan="2">{{ $t('pm.final.abilityview') }}</th>
        <th class="text-center fixedHeader sticky-th" rowspan="2">{{ $t('pm.final.totalLevel') }}</th>
      </tr>
      <tr>
        <th class="text-center fixedHeader2 sticky-th-two">{{ $t('pm.final.goaltable2') }}</th>
        <th class="text-center fixedHeader2 sticky-th-two">{{ $t('pm.final.goaltable3') }}</th>
        <th class="text-center fixedHeader2 sticky-th-two">{{ $t('pm.final.goaltable2') }}</th>
        <th class="text-center fixedHeader2 sticky-th-two">{{ $t('pm.final.goaltable3') }}</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(item, item_idx) in empListBySort">
        <tr v-if="lvStatus[item.finalLevel] || !item.finalLevel " :key="item_idx" class="emp-by-sort">
          <td class="text-center"></td>
          <td><img :src="item.avatarUrl" class="table_avatar" />{{ item.empNm }}</td>
          <td class="text-center">{{ lvStr[item.finAvSelfLv] }}</td>
          <td class="text-center txt-700">{{ lvStr[item.finAvMentorLv] }}</td>
          <td class="text-center">{{ `${item.compSfLv ? 'Level ' + item.compSfLv : ''}` }}</td>
          <td class="text-center txt-700">{{ `${item.compMtLv ? 'Level ' + item.compMtLv : ''}` }}</td>
          <td class="text-center txt-700 text-primary">{{ item.finalLevel }}</td>
        </tr>
      </template>
    </tbody>
  </table>
</div>
```

**CSS**

```css
.table-wrapper {
  overflow-y: auto;
  border-collapse: collapse;
  height: 500px;
  padding-top: 0px;
}

.result-table {
  margin: 0px;
}

.result-table td {
  text-align: center;
}

.result-table thead .sticky-th {
  position: sticky;
  top: 0px;
}
.result-table thead .sticky-th-two {
  position: sticky;
  top: 38px;
}

.result-table thead .sticky-th:after {
  content: '';
  position: absolute;
  left: 0;
  width: 1px;
  height: 76px;
  background: #dee2e6;
}
.result-table thead .sticky-th:before {
  content: '';
  position: absolute;
  left: 0;
  width: 100%;
  height: 2px;
  background: #dee2e6;
}
.result-table thead .sticky-th:after {
  top: 0px;
}
.result-table thead .sticky-th:before {
  top: -1px;
}

.result-table thead .sticky-th-two:after {
  content: '';
  position: absolute;
  top: -2px;
  left: 0;
  width: 100%;
  height: 2px;
  background: #dee2e6;
}
.result-table thead .sticky-th-two:before {
  content: '';
  position: absolute;
  left: 0;
  width: 1px;
  height: 38px;
  background: #dee2e6;
}
.result-table thead .sticky-th-two:after {
  top: -2px;
}
.result-table thead .sticky-th-two:before {
  bottom: 0px;
}
```
