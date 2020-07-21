---
layout: post
title:  "AWS RDS 인코딩 UTF8 설정하기"
description: "AWS RDS 한글 입력 문제가 있을 때는 인코딩을 설정하자"
# date:   2020-07-20 19:27:36 +0530
categories: AWS RDS DB 
---

![image](https://user-images.githubusercontent.com/18201794/88006921-c49d9680-cb47-11ea-9fb0-e7fb743f16ad.png)

AWS RDS를 이용해 MariaDB를 설치하면 Default 인코딩이 UTF-8이 아닌 latin-1로 설정되어 있다. 그렇기 때문에 RDS DB에 한글을 삽입하는 경우 에러가 발생하거나 한글이 깨지는 오류가 발생한다.  
위와 같은 상황에서 DB의 인코딩을 UTF-8로 변경하여 한글 깨짐 현상을 해결할 수 있다.

---

1. AWS Management Console에 접속후 RDS 이동  

2. 좌측 메뉴에 파라미터 그룹 -> 파라미터 그룹 생성

3. 파라미터 그룹 패밀리 - 해당하는 버전 선택  
   그룹명 / 설명 입력

4. 생성완료 후 파라미터 그룹 선택

5. 검색창에 character_set 검색 후 파라미터 편집

6. 모든 character set의 값을 utf8로 변경. 변경 후 저장

7. 해당 DB인스턴스로 이동 후

8. 인스턴스 작업 -> 수정

9. 데이터베이스 옵션 -> 만든 파라미터 그룹 선택 

10. 즉시적용 선택 후 DB인스턴스 수정 클릭

11. 인스턴스 재부팅

12. **show variables like 'c%';** 쿼리를 활용해 변경 사항 확인

---


위 과정을 통해 DB의 인코딩 설정을 바꿀 수 있다.  
하지만 설정 후의 테이블에 해당해서 적용이 되며 이전 테이블은 적용되지 않을 수 있다.  
아래 쿼리를 활용해 테이블의 인코딩을 직접 변경할 수 있다.  

```SQL
alter table [테이블명] convert to character set utf8;
```

