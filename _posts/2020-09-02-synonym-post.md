---
layout: post
title:  "Synonym"
date:   2020-09-02 02:59:13 +0800
categories: DB
tags: db
---
<p>
Synonym은 오라클 객체(테이블, 뷰, 시퀀스, 프로시저)에 대한 <storng>대체이름(Alias)</strong>를 말하며, 실질적으로 그 자체가 객체가 아니라 객체에 대한 직접적인 참조이다.<br>
</p>

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

<p><strong>Synonym 예제</strong></p>
<p>scott USER의 emp테이블을 test USER가 사용 하는 예제</p>
<code>
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
</code>


