---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 7주차 후기"
description: >-
  Docker 를 사용한 MySQL 서버 연결 및 SQL 실습
author: gisoun
date: 2025-08-14 17:46:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, database, mysql, sql]
pin: false
media_subpath: '/assets/posts/20250814'
published: true
---

> 2025\. 8\. 11\. ~ 2025\. 8\. 14\.

---

지난 주차를 마지막으로 **`HTML/CSS/JS 및 TS`**, **`React`**, **`React Native`** 강의가 마무리 되었습니다. 짧은 기간 내에 미니 프로젝트를 포함한 정말 값진 경험을 할 수 있었습니다.  

이에 강사님께도 감사 인사를 전합니다! (_ _)  

이번 주차부터는 새로운 강사님과 함께 **`관계형 데이터베이스 학습`** 및 **`SQL 실습`**을 시작으로 **`Node.js`** 기반 백엔드 개발을 목표로 하게 되었습니다.  

새로운 첫 주차인 만큼 **`MySQL`** 환경 구축과 간단한 SQL 예제 실습만을 하였습니다.

---

## Docker 기반 MySQL 서버 실행

저는 로컬 저장소에 직접 **`MySQL`**을 설치하는 대신, **`Docker`**를 사용하여 **가상화된 컨테이너 환경**에 **`MySQL`**을 설치하고 실행하였습니다.

### MySQL Docker 이미지 가져오기

먼저, **Windows PowerShell** 을 열고 아래 명령어를 입력하여 **`MySQL 8.4.6 버전`**을 **`Docker`** 이미지로 가져옵니다. 8.4 이상 버전을 선택한 이유는 [Oracle에서 장기 지원(LTS, Long-Term Support)을 보장하는 버전](https://dev.mysql.com/doc/relnotes/mysql/8.4/en/news-8-4-6.html)이기 때문에, 안정성과 보안성 면에서 신뢰할 수 있기 때문입니다.  

```powershell
docker pull mysql:8.4.6
```

**`MySQL`** 이미지가 정상적으로 설치되었는지, 아래 명령어로 **`mysql`** 이미지를 필터링하여 확인해 보겠습니다.  

```powershell
docker images --filter "reference=mysql"
```

![image](docker-images-1.png)
_정상적으로 설치된 MySQL Docker 이미지_

**`mysql`** 이미지가 목록에 나타난 것으로 보아, 성공적으로 설치되었음을 알 수 있습니다.

### Docker 컨테이너 실행

이미지를 성공적으로 내려받았으니, 이제 해당 이미지를 사용하여 **`Docker`** 컨테이너를 실행할 차례입니다. 아래 명령어는 컨테이너의 **`3306`** 포트를 로컬 머신의 **`3306`** 포트와 연결하고, **`MySQL root 계정`**의 비밀번호(**`root_password`**)를 설정합니다.  

> **`root_password`** 를 실제 사용할 비밀번호로 변경하여 사용해야 합니다!
{: .prompt-info }

```powershell
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=root_password -d -p 3306:3306 mysql:8.4.6
```

이제 컨테이너가 잘 실행되고 있는지도 확인해 봐야겠죠? 아래 명령어를 통해 **`mysql-container`** 가 현재 실행 중인 컨테이너 목록(PROCESS STATUS)에 있는지 확인합니다.  

```powershell
docker ps
```

![image](docker-ps-1.png)
_정상적으로 실행 중인 `mysql-container` 컨테이너_

**`mysql-container`** 컨테이너 역시 잘 실행되고 있네요!


### 로컬이 아닌 Docker를 사용한 이유?

- **`독립적인 환경`**: **`Docker`** 를 사용하면 내 PC(로컬)와 완전히 분리된 독립적인 환경에 **`MySQL`**을 설치할 수 있습니다. 이를 통해 버전 충돌 문제를 원천적으로 방지하고, 로컬 저장소가 지저분해지는 것을 막을 수 있습니다.  
   개인적으로 예전에 개발할 때 이러한 버전 충돌 문제로 발목 잡힌 적인 한두번이 아닌지라 특히나 Docker 를 자주 사용하게 되는 것 같습니다...
- **`손쉬운 관리`**: 컨테이너를 삭제하면 **`MySQL`** 서버도 깔끔하게 삭제되므로, 설치와 제거가 매우 간편합니다!
- **`일관성 있는 환경`**: 추후 협업 또는 팀 프로젝트를 진행할 때, 프로젝트팀 전체가 동일한 **`Docker`** 이미지를 공유하여, 모든 팀원이 동일한 버전과 설정의 데이터베이스 환경에서 개발을 진행할 수 있습니다.

---

## DBeaver 설치 및 컨테이너 연결

이제 **`Docker`** 로 실행한 **`MySQL`** 서버에 접속하여 데이터를 관리할 **`DBMS(Database Management System)`** 도구를 설치해 보겠습니다. 강의에선 [**MySQL Workbench**](https://www.mysql.com/products/workbench/) 를 사용하였지만, 저는 더 넓은 범용성과 확장성을 지닌 강력한 오픈 소스 도구 [**DBeaver**](https://dbeaver.io/)를 사용하였습니다.  

[**DBeaver**](https://dbeaver.io/) 공식 홈페이지에서 커뮤니티 버전(**Community Edition**)을 다운로드하여 설치를 진행합니다.

![image](dbeaver-1.png)
_설치된 DBeaver_

### DBeaver의 장점

- **`다양한 DB 지원`**: **`MySQL`** 또는 **`MariaDB`** 에 특화된 **MySQL Workbench** 에 비해 **`PostgreSQL`**, **`Oracle`** 등 수많은 종류의 데이터베이스 연결을 지원하기에 추후 확장에 용이할 것으로 생각됩니다.
- **`무료 및 오픈소스`**: 커뮤니티 버전은 **무료**로 제공되며, 누구나 자유롭게 사용할 수 있습니다.
- **`직관적인 UI`**: **개발자 친화적인 UI**와 **강력한 쿼리 편집기**, **데이터 시각화 도구** 등을 제공하여 생산성을 높여줍니다.

### MySQL 컨테이너 연결 테스트

설치한 DBeaver 를 실행하고, **`Docker`**에서 실행 중인 **`mysql-container`** 에 접속해 보겠습니다.  

1. DBeaver 상단 메뉴에서 **<kbd>데이터베이스</kbd>** **>** **<kbd>새 데이터베이스 연결</kbd>** 선택  
   
   ![image](dbeaver-2.png)
   _[데이터베이스] > [새 데이터베이스 연결] 선택_

2. **MySQL** 을 선택하고 **<kbd>다음</kbd>** 버튼 클릭  
   
   ![image](dbeaver-3.png)
   _MySQL 선택_

3. 서버 호스트는 **`localhost`** (또는 127.0.0.1), 포트는 **`3306`**, 사용자명은 **`root`**, 비밀번호는 위에서 docker run 명령어 실행 시 설정했던 **`root_password`** 를 입력  
   
   ![image](dbeaver-4.png)
   _서버 호스트 및 사용자 정보 입력_

4. 왼쪽 하단의 <kbd>Test Connection ...</kbd> 버튼을 클릭하여 연결 테스트  
   
   ![image](dbeaver-5.png)
   _데이터베이스 연결 테스트_

   연결 정보가 정확하다면, 위와 같이 성공적으로 연결되었다는 팝업창이 나타납니다.

이것으로 DBMS 내에서의 준비도 끝났습니다!

---

## 실습

위에서 구축한 **`MySQL`** 컨테이너 환경을 통해 간단한 예제를 실습하는 것으로 이번 포스팅을 마치겠습니다.

### 예제 1

**`Employees`** 테이블을 생성하고 데이터를 추가한 후, 특정 조건에 따라 데이터를 삭제하는 **DML(데이터 조작 언어)** 및 **DDL(데이터 정의 언어)** 예제입니다.

- **`요구사항`**  
   
   1. 사번, 이름, 연봉 컬럼을 가진 **`Employees`** 테이블을 생성합니다.
   2. 10개 이상의 데이터를 추가합니다.
   3. 8번째 사원을 삭제(퇴사) 처리합니다.

- **`쿼리 실행`**  
   
   ```sql
   -- gisoundb 데이터베이스 사용
   use gisoundb;
   
   -- department 테이블 생성
   create table department (
     department_id bigint not null auto_increment,
     department_name varchar(100) default null,
     primary key (department_id)
   ) engine=InnoDB auto_increment=0 default CHARSET=utf8mb4 collate=utf8mb4_0900_ai_ci;
   
   -- department 데이터 추가
   insert into department (department_name) values ('개발');
   insert into department (department_name) values ('기획');
   insert into department (department_name) values ('경영');
   insert into department (department_name) values ('재무');
   
   -- employees 테이블 생성
   create table employees (
     employee_id bigint not null auto_increment,
     name varchar(100) default null,
     salary decimal(10,2) default null,
     department_id bigint default null,
     hire_date date default null,
     primary key (employee_id)
   ) engine=InnoDB auto_increment=0 default CHARSET=utf8mb4 collate=utf8mb4_0900_ai_ci;
   
   -- employees 데이터 추가
   insert into employees (name, salary, department_id, hire_date) values ('이기순', 4500, 1, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('박인천', 3000, 2, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('최검단', 3850, 3, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('유당하', 3000, 3, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('박광역', 3000, 4, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('박송도', 3200, 4, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('김기순', 4800, 2, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('윤빛가람', 3800, 2, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('서구', 4500, 1, NOW());
   insert into employees (name, salary, department_id, hire_date) values ('천불로', 3600, 1, NOW());
   
   -- 8번째 사원 삭제
   delete from employees where employee_id = 8;
   
   -- 최종 데이터 확인
   select * from employees;
   ```

### 예제 2

이번에는 도서 관리 시스템을 가정하여 **`Books`** 테이블을 생성하고, 특정 조건에 따라 데이터를 수정하는 **UPDATE** 구문 예제입니다.

- **`요구사항`**  
   
   1. 책 ID, 제목, 저자, 가격, 재고 수량을 가진 **`Books`** 테이블을 생성하고 15권의 책 데이터를 입력합니다.
   2. 가격이 20,000원 미만인 모든 책의 가격을 10% 인상합니다.
   3. **'김영하'** 저자의 책 중 재고가 5개 미만인 책들의 재고를 10개로 업데이트합니다.

- **`쿼리 실행`**
   
   ```sql
   -- gisoundb 데이터베이스 사용
   use gisoundb;
   
   -- books 테이블 생성
   create table books (
       book_id bigint auto_increment not null comment 'PK',
       title varchar(1000) null comment '책 제목',
       author varchar(100) null comment '저자',
       price int null comment '책 가격',
       stock int null comment '책 재고 수량',
       constraint books_pk primary key (book_id)
   )
   engine=InnoDB
   default CHARSET=utf8mb4
   collate=utf8mb4_0900_ai_ci;
   
   -- books 데이터 추가 (15권)
   insert into books (title, author, price, stock) values ('어린 왕자', '앙투안 드 생텍쥐페리', 18500, 45);
   insert into books (title, author, price, stock) values ('데미안', '헤르만 헤세', 21000, 32);
   insert into books (title, author, price, stock) values ('1984', '조지 오웰', 32000, 28);
   insert into books (title, author, price, stock) values ('위대한 개츠비', 'F. 스콧 피츠제럴드', 11000, 25);
   insert into books (title, author, price, stock) values ('호밀밭의 파수꾼', 'J.D. 샐린저', 13500, 9);
   insert into books (title, author, price, stock) values ('노인과 바다', '어니스트 헤밍웨이', 20800, 5);
   insert into books (title, author, price, stock) values ('해리 포터와 마법사의 돌 1', 'J.K. 롤링', 19800, 110);
   insert into books (title, author, price, stock) values ('반지의 제왕 1: 반지원정대', 'J.R.R. 톨킨', 19500, 17);
   insert into books (title, author, price, stock) values ('오만과 편견', '제인 오스틴', 30000, 20);
   insert into books (title, author, price, stock) values ('랄랄라 하우스', '김영하', 23000, 20);
   insert into books (title, author, price, stock) values ('여행의 이유', '김영하', 19800, 11);
   insert into books (title, author, price, stock) values ('빛의 제국', '김영하', 19500, 3);
   insert into books (title, author, price, stock) values ('햄릿', '윌리엄 셰익스피어', 10000, 17);
   insert into books (title, author, price, stock) values ('검은 꽃', '김영하', 22000, 19);
   insert into books (title, author, price, stock) values ('돈키호테 1', '미겔 데 세르반테스', 21000, 13);
   
   -- 가격이 20000원 미만인 책 가격 10% 인상
   update books
   set price = price * (1 + 0.1)
   where price < 20000;
   
   -- 재고가 5개 미만인 책 재고를 10개로 업데이트
   update books
   set stock = 10
   where stock < 5;
   
   -- 최종 데이터 확인
   select * from books;
   ```

### 예제 3

새로운 사용자를 생성하고 특정 테이블(**`gisoundb.employees`**)에 대한 권한을 부여하는 **DCL(데이터 제어 언어)** 예제입니다.

- **`요구사항`**  
   
   1. 자신의 이름 이니셜로 새로운 사용자를 만듭니다.
   2. 해당 사용자에게 **`Employees`** 테이블에 대한 **SELECT**, **INSERT** 권한을 부여합니다.
   3. 해당 사용자로 접속하여 새로운 행을 추가(**INSERT**)합니다.

- **쿼리 실행**  
   
   ```sql
   -- 'new_gisoun' 사용자 생성 및 비밀번호 설정
   CREATE USER 'new_gisoun'@'localhost' IDENTIFIED BY 'new_gisoun_password';
   
   -- 'new_gisoun' 사용자에게 gisoundb.employees 테이블에 대한 SELECT, INSERT 권한 부여
   GRANT SELECT, INSERT ON gisoundb.employees TO 'new_gisoun'@'localhost';
   ```

### 예제 4

사용자 생성 및 권한 부여, 데이터 추가 및 수정을 종합적으로 실습하는 예제입니다.

- **`요구사항`**  
   
   1. **`'product_admin'`** 사용자를 생성하고 비밀번호를 **`'prod1234'`** 로 설정합니다.
   2. 해당 사용자에게 **`'shop_db'`** 데이터베이스의 **`'products'`** 테이블에 대한 모든 권한을 부여합니다.
   3. **`'products'`** 테이블에 제품 정보를 4개 이상 추가합니다.
   4. 가격이 5,000원 이상인 제품의 가격을 10% 인상합니다.
   5. 제품 조회 전용 사용자인 **`'product_viewer'`** 를 생성하고 조회 권한만 부여합니다.

- **`쿼리 실행`**
   
   ```sql
   -- shop_db 데이터베이스 생성 및 사용
   create database shop_db;
   use shop_db;
   
   -- products 테이블 생성
   create table products (
       id bigint auto_increment not null comment 'PK',
       name varchar(100) null comment '제품명',
       price int null comment '제품 가격',
       category varchar(100) null comment '제품 카테고리',
       constraint products_pk primary key (id)
   )
   engine=InnoDB
   default CHARSET=utf8mb4
   collate=utf8mb4_0900_ai_ci;
   
   -- 'product_admin' 사용자 생성 및 권한 부여
   create user 'product_admin'@'localhost' IDENTIFIED by 'prod1234';
   grant all privileges on shop_db.products to 'product_admin'@'localhost';
   
   -- 변경사항 적용
   flush privileges;
   
   -- 제품 데이터 추가
   insert into products (name, price, category) values ('제품 001', 4500, '식품');
   insert into products (name, price, category) values ('제품 002', 98000, '의류');
   insert into products (name, price, category) values ('제품 003', 10000, '상품권');
   insert into products (name, price, category) values ('제품 004', 23800, '의류');
   insert into products (name, price, category) values ('제품 005', 1500, '식품');
   
   -- 가격이 5000 이상인 제품 가격 10% 인상
   update products
   set price = price * (1 + 0.1)
   where price >= 5000;
   
   -- 'product_viewer' 사용자 생성 및 SELECT 권한 부여
   create user 'product_viewer'@'localhost' IDENTIFIED by 'product_viewer_password';
   grant select on shop_db.products to 'product_viewer'@'localhost';
   ```

### 예제 5

집계 함수와 날짜 및 시간 함수를 활용하여 데이터를 분석하는 예제입니다.

- **`요구사항`**  
   
   1. 직원들의 평균 급여를 계산하세요.
   2. 2023년에 입사한 직원 수를 구하세요.
   3. 부서별 최고 급여와 최저 급여의 차이를 계산하세요.

- **`쿼리 실행`**
   
   ```sql
   -- gisoundb 데이터베이스 사용
   use gisoundb;
   
   -- 1) 직원 평균 급여
   select AVG(salary) as avg_salary
   from employees;
   
   -- 2) 2023년에 입사한 직원 수
   select count(*) as cnt
   from employees
   where year(hire_date) = 2023;
   
   -- 3) 부서별 최고 급여와 최저 급여의 차이
   select
       department_id,
       max(salary) - min(salary) as salary
   from employees
   group by department_id;
   ```

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
