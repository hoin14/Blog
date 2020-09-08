---
layout: post
title:  "[Oracle] 권한관리"
date:   2020-09-05 02:59:13 +0800
categories: Db
tags: db
---

###### 권한(Privileges) 관리
<p>
권한이란 데이터베이스에 접속하거나 데이터베이스의 객체에 접근 하거나 SQL문을 실행 할 수 있도록 스키마객체에 부여된 설정들이다. DBA가 유저 객체에 직접 부여할 수 도 있고 ROLE(시스템 권한,객체 권한을 저장하고 있는 객체)을 생성하여 롤에 권한을 부여한 뒤 그 룰을 유저에게 할당하는 간접적인 방법이 있다. 권한에는 오브젝트 권한(Object Privilege)와 시스템 권한(System Privilege)가 있다.
</p>

<p><strong>시스템 권한(System Privilege)</strong></p>
<p>
시스템 권한은 DBMS에 대한 전반적인 관리 작업에 필요한 권한을 말한다. 이러한 작업에는 테이블, 뷰, 인덱스, 프로시저등의 객체에 대한 생성, 삭제 수정 작업들이 있다. 시스템 권한은 주로 DBA가 부여하며 system_privilege_map 뷰를 전체 시스템 권한을 통해 확인할 수 있다. 시스템 권한을 분류해 보면 CREATE SESSION, CREATE TABLESPACE 처럼 전 시스템에 영향을 주는 것과 CREATE TABLE처럼 사용자 자신의 스키마 오브젝트에 대한 관리를 가능하게 해주는 권한이 있다. 
</p>

<p>
<strong>※주요 시스템 권한</strong><br>
- CREATE SESSION : DB에 연결할 수 있는 권한<br>
- CREATE TABLE : user소유 스키마 안에서 테이블 또는 인덱스를 생성할 수 있는 권한<br>
- SELECT ANY TABLE : 어떤 스키마에서나 모든 테이블, 뷰에 대한 검색 권한<br>
- ALTER SYSTEM : 시스템 정의를 변경할 수 있는 권한<br>
- CREATE ROLE : 오라클 데이터베이스 ROLE을 생성할 수 있는 권한<br>
- INSERT ANY TABLE : 어떤 스키마에서나 모든 테이블, 뷰에 데이터를 입력할 수 있는 권한<br>
- CREATE USER : 유저를 생설할 수 있는 권한<br>
- ALTER USER: 유저의 정의를 변경할 수 있는 권한<br>
- DROP USER : 유저를 삭제시킬 수 있는 권한<br>
- DROP ANY TABLE : 테이블을 TRUNCATE 할 수 있는 권한<br>
</p>

<p>
<strong>・시스템 권한 부여</strong><br>
GRANT문을 이용하여 시스템 권한을 유저나 롤에 주로 DBA가 부여한다.TO 뒤에 권한을 받을 유저나 롤을 지정한다.WITH ADMIN OPTION은 해당 시스템 권한을 다른 사용자나 롤에 재부여 할 수 있도록 허용한다. 시스템 권한은 DB정의를 변경할 수 있기 때문에 권한 부여시 주의가 필요하다.
</p>
```
SQL>GRANT CREATE TABLE, CREATE VIEW TO scott;
SQL>SELECT GRANTEE, PRIVILEGE, ADMIN_OPTION FROM DBA_SYS_PRIVS WHERE GRANTEE = 'HR';
SQL>SELECT USERNAME, PRIVILEGE, ADMIN_OPTION FROM USER_SYS_PRIVS;
```
<p>
<strong>・시스템 권한 회수</strong><br>
</p>
```
SQL>REVOKE CREATE TABLE, CREATE VIWE FROM 'HR';
SQL>SELECT GRANTEE, PRIVILEGE, ADMIN_OPTION FROM DBA_SYS_PRIVS WHERE GRANTEE = 'HR';
```

<p><strong>객체 권한(Object Privilege)</strong></p>
<p>
객체권한 이란 특정한 Table, View, Sequenece, Procedure, Function, Package등의 DB Object에 대해서 SELECT, INSERT, EXECUTE 같은 특정 작업을 수행하는 권한이다. 객체에 대해 권한 부여 및 회수 방법은 SYSTEM권한과 유사하며 다만 대상 객체를 명시한다는 점이 다르다. 객체의 소유자는 객체에 대한 모든 권한을 가진다. 객체 권한을 부여하기 위해서는 객체의 소유자이거나 WITH ADMIN OPTIN으로 권한을 부여 받아야 한다.
</p>
<p>
<strong>※주요 오브젝트 권한</strong><br>
</p>
<p>
ALTER : 테이블, 시퀀스에 적용되며 객체를 변경할 수 있도록 함<br>
DELETE : 테이블, 뷰에 적용되며 Data를 Delete할 수 있는 권한<br>
EXECUTE : procedure, function, package에 대해 실행할 수 있도록 허용<br>
INDEX : 권한을 받은 사용자가 table에 대해 인덱스를 생성할 수 있도록 허용<br>
INSERT : 테이블과 뷰에 대해서 데이터를 insert할 수 있도록 허용<br>
REFERENCES : 테이블에 대한 Fkey를 생성할 수 있는 권한<br>
SELECT : 테이블, 시퀀스에 대한 조회 권한<br>
AUDIT : 권한을 받은 사용자가 감시를 할 수 있도록 허용<br>
COMMENT : 권한을 받은 사용자가 주석을 달 수 있도록 허용<br>
LOCK : 권한을 받은 사용자가 locking할 수 있도록 허용<br>
</p>

<p>
<strong>・객체 권한 부여</strong><br>
</p>
<p>
권한을 부여하려면 객체가 자신의 스키마에 있거나 WITH GRANT OPTION권한을 갖고 있어야 한다. SYSTEM 권한과 마찬가지로 GRANT문을 사용하지만 ON구 다음에 대상 객체를 명시한다는 점이 다르다. GRANT절 뒤에는 권한을 일일이 나열하는 대신에 ALL이라는 키워드를 사용하여 ON 뒤에 나오는 객체에 대해서 모든 객체 권한을 한꺼번에 부여할 수 있다. INSERT, UPDATE, REFERENCES권한은 Table 전체가 아닌 특정 칼럼에 대해 지정이 가능하다. 다른 사용자에 대해 권한을 부여하려면 스키마.객체명 형식을 사용한다. 
</p>
```
SQL>GRANT CONNECT, RESOURCE TO HR WITH GRANT OPTION;
SQL>GRANT UPDATE(ename, sal) ON emp TO HR WITH GRANT OPTION;
```

<p>
<strong>・객체 권한 회수</strong><br>
</p>
```
SQL>REVOKE execute ON dbms_pipe FROM HR;
```

<p>
<strong>・객체 권한 조회</strong><br>
</p>
<p>
데이터베이스 내의 모든 객체 권한을 보여주는 딕셔너리 뷰인 DBA_TAB_PRIVS와 칼럼에 지정된 모든 객체 권한은 DBA_COL_PRIVS을 이용하여 객체 권한 내역을 확인 할 수 있다.
</p>
```
-사용자의 객체에 대한 권한 부역내역 조회
SQL>SELECT GRANTEE, OWNER, TABLE_NAME, GRANTOR, PRIVILEGE, GRANTABLE, HIERARCHY FROM USER_TAB_PRIVS;

-사용자의 객체에 대한 권한 부역내역 조회
SQL>SELECT GRANTEE, OWNER, TABLE_NAME, GRANTOR, PRIVILEGE, GRANTABLE FROM USER_COL_PRIVS;

-부여받은 객체 권한 확인
SQL>SELECT OWNER, TABLE_NAME, GRANTOR, PRIVILEGE, HIERARCHY FROM USER_TAB_PRIVS_RECD;

-사용자가 부여한 객체권한 내역 조회
SQL>SELECT GRANTEE, OWNER, TABLE_NAME, GRANTOR, PRIVILEGE, GRANTABLE, HIERARCHY FROM ALL_TAB_PRIVS_MADE;
```
<p>
EXAMPLE
</p><br>

```
SQL> conn /as sysdba
SQL> create user test identified by test;
SQL> grant create session to test;
SQL> revoke create session from test;
SQL> grant resource to test;
SQL> grant connect to test;
SQL> conn test/test
SQL> show user
SQL> select grantee, privilege from dba_sys_privs where grantee = 'CONNECT';
SQL> select grantee, privilege from dba_sys_privs where grantee = 'RESOURCE';
```

<p>
권한 검색은 sys유저로 확인해야 함.
</p><br>

<p>
사용자에게 부여된 시스템 권한 확인
</p>
```
SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE = '사용자명';
```
<p>
사용자에게 부여된 롤 확인
</p>
```
SELECT * FROM DBA_ROLE_PRIVS WHERE GRANTEE = '사용자명';
```
<p>
사용자에게 부여된 롤에 대한 시스템 권한 확인ㅇ
</p>
```
SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE = '롤명';
```
<p>
타 사용자에게 부여된 객체 권한 확인
</p>
```
SELECT * FROM DBA_TAP_PRIVS WHERE OWNER = '테이블 소유자명';
```


