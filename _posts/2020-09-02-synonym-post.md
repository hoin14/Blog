---
layout: post
title:  "오라클 Synonym, View"
date:   2020-09-02 02:59:13 +0800
categories: DB
tags: db
---
##### 오라클 Synonym

<p>
Synonym은 오라클 객체(테이블, 뷰, 시퀀스, 프로시저)에 대한 <strong>대체이름(Alias)</strong>를 말하며, 실질적으로 그 자체가 객체가 아니라 객체에 대한 직접적인 참조이다.</p>
<br>
<p><strong>Synonym을 사용하는 이유</strong></p>
<ul>
<li>
<p>데이터베이스의 투명성을 제공하기 위해서 사용 한다. Synonym은 다른 유저의 객체를 참조할 때 많이 사용을 한다.</p>
</li>
<li>
<p>다른 유저의 객체를 참조할 경우가 있을 때 Synonym을 생성해서 사용을 하면 추후에 참조하고 있는 Object가 이름을 바꾸거나 이동할 경우 객체를 사용하는 SQL문을 모두 다시 고치는 것이 아니라 Synonym만 다시 정의하면 된다</p>
</li>
<li>
<p>객체를 참조하는 사용자의 Obejct를 감추 수 있기 때문에 보안을 유지할 수 있다.</p>
</li>
</ul>
<br>
<p><strong>Synonym 예제</strong></p>
<p>scott USER의 emp테이블을 test USER가 사용 하는 예제</p>

```
-- ① 먼저 scott/tiger USER로 접속해서 test USER에게 
--   emp 테이블을 조작할 권한을 부여합니다.
SQL> GRANT ALL ON  emp TO test; 

-- ② test USER로 접속해 동의어를 생성합니다. 
SQL> CONNECT test/test 
SQL> CREATE SYNONYM scott_emp FOR scott.emp ; 

-- scott USER가 소유하고 있는 emp 테이블에 대해 
   scott_emp라는 일반 시노님을 생성했다. 
-- scott 사용자의 emp테이블을 test 사용자가 
   scott_emp라는 동의어로 사용 합니다. 

-- ③ 시노님을 이용한 쿼리
SQL> SELECT empno, ename FROM  scott_emp; 

-- 일반 테이블을 쿼리
SQL> SELECT empno,  ename FROM  scott.emp; 
 이 두 쿼리의 결과는 같다. 

   EMPNO ENAME
-------- ---------
    7369 SMITH
    7499 ALLEN
...

-- ④ 동의어 삭제 
SQL> DROP SYNONYM scott_emp; 

-- 시노님을 이용한 조회
SQL> SELECT empno,  ename FROM  scott_emp; 
         라인 1 에 오류:
     ORA-00942: 테이블 또는 뷰가 존재하지 않습니다 
```

##### 오라클 View

<p>
View는 사용자에게 접근이 허용된 자료만을 제한적으로 보여주기 위해 하나 이상의 기본 테이블로부터 유도된,이름을 가지는 <strong>가상 테이블</strong>이다.<br>
</p>
<br>
<p><strong>View의 특징</strong></p>
<ul>
<li>
<p>View는 기본테이블로부터 유도된 테이블이기 때문에 기본 테이블과 같은 형태의 구조를 사용하며, 조작도 기본 테이블과 거의 같다.</p>
</li>
<li>
<p>View는 가상 테이블이기 때문에 물리적으로 구현되어 있지 않다.</p>
</li>
<li>
<p>필요한 데이터만 View로 정의해서 처리할 수 있기 때문에 관리가 용이하고 명령문이 간단해진다.</p>
</li>
<li>
<p>View를 통해서만 데이터에 접근하게 하면 뷰에 나타나지 않는 데이터를 안전하게 보호하는 효율적인 기법으로 사용할 수 있다.</p>
</li>
</ul>
<br>
<p><strong>View 예제</strong></p>
<p>scott USER의 emp테이블을 test USER가 사용 하는 예제</p>

```
--문법--
CREATE VIEW 뷰이름[(속성이름[,속성이름])]AS SELECT문;

--고객 테이블에서 주소가 서울시인 고객들의 성명과 전화번호를 서울고객이라는 뷰로 만들어라--
CREATE VIEW 서울고객(성명, 전화번호)
AS SELECT 성명 전화번호
FROM 고객
WHERE 주소 = '서울시'; 

--문법--
DROP VIEW 뷰이름 RESTRICT or CASCADE

--서울고객이라는 뷰를 삭제해라--
DROP VIEW 서울고객 RESTRICT;
```

