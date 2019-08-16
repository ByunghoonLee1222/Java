# DDL(Data Definition Language)

* **Primary** **key**(주키)
  * 행 데이터를 구별할 목적으로 사용하는 키
  * 데이터 중복되지 않고 null이 없어야 한다
  * 성능이 느리다
* **Unique**
  * 중복되지 않은 데이터만 저장할 경우
  * 중복데이터 저장 시error
* **Not null**
  * null이 없는 데이터
  * null 데이터 저장하면 error
  * 컬럼 레벨에서만 설정 가능
* **Foreign** **key**(외래키)
  * 다른 테이블의 primary key데이터를 참조
  * 부모키에 없는 데이터를 입력하면 오류
  * 부모키 삭제시 오류 발생



* **create**
* **drop**
* **alter**

```mysql

/*
	날짜 기본값 설정 5.6.5 미안은 now()
				5.6.5 이상은 current_timestamp
                => 년,월,일,시,분,초로 설정되므로 타입은 datetime 또는 timestamp로 지정해야 한다.
*/
create table semp(
	empno 		int auto_increment primary key
    ,name 		varchar(50)
    ,sal 		int
    ,hiredate 	datetime default current_timestamp
    ,deptno 	int
);

create table member(
	id			varchar(30) primary key
    ,password	varchar(30) not null
    ,email		varchar(50)
    ,phone		varchar(16)
    ,address	varchar(200)
	
);
-- 설명
create table orders(
	ono			int 		 auto_increment primary key
    ,odate 		datetime 	 default current_timestamp
    ,id 		varchar(30) -- references member(id)
    ,gno 		int			 not null
    ,quantity 	int			 default 1
    ,address 	varchar(200)
    ,foreign key fk_orders_id(id)  references member(id) 
    ,foreign key fk_orders_gno(gno) references goods(gno) 
);
/*
check 제약 조건
- insert, update할 때 지정한 조건에 맞지 않으면 error 발생
형식]
[constraint 제약조건명] check( 컬럼명 조건)
*/
create table cemp(
	empno				int				primary key
    ,ename				varchar(30)		not null
    ,sal 				int 			default 1500
    ,commission_pct		numeric(4,2)
    ,constraint check	(commission_pct in (10, 10.5,12,12.5,15))
    ,constraint check	(sal>=1000)
);

/*
테이블 변경
alter table 테이블명	add|modify|change|drop 컬럼명
*/
-- 컬럼 추가 alter table 테이블명 add 컬럼명 타입

alter table cemp add deptno int;
desc cemp;

-- 컬럼 타입 변경 alter table 테이블명 modify 컬럼명 타입
alter table cemp modify deptno varchar(30);

-- 컬럼 이름 및 타입 변경
-- alter table 테이블명 change 이전 칼럼명 변경할_컬럼이름 변경할 타입;
alter table cemp change deptno address varchar(30);


-- 컬럼 삭제 		alter table 테이블명 drop 컬럼명;
alter table cemp drop address;

desc cemp;

/* 테이블 삭제
형식] drop table 테이블명;
주의점] 자식테이블이 있는 부모테이블인 경우 삭제 안됨
		=> 자식테이블을 삭제 후 부모테이블을 삭제 해야 한다.
*/
drop table goods;	-- orders 테이블이 참조하고 있어서 삭제 안됨

drop table cemp;	-- cemp는 참조하는 테이블이 없어서 삭제 된다.

-- 테이블의 구조와 데이터 복제하기
-- create table 테이블명 as select문
-- select 문을 수행된 결과 테이블이 복제됨

create table cemp as select empno,ename,sal,deptno
from emp;

select *
from cemp;


/*
truncate
- 테이블의 모든 데이터를 삭제
- 복구할 수 없다
형식] truncate 테이블명;
*/
truncate cemp;
rollback;
```



