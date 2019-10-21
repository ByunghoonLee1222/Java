# Index & View

```mysql
/*
	index
- 자주 조회하는 컬럼에 인덱스를 부여
- join이 많을 때도 유리
- 검색 속도 향상 (nlogn 보다 빠르다)
- DML 작업이 많을 때는 비효율적 (계속해서 새로 생성)
- 단일 컬럼뿐아니라 복합 컬럼으로도 만들 수 있다
    -- mysql은 primary
*/

create index idx_goods_brand on goods(brand);

select * from emp;

-- empno가 클러스터 인덱스이므로 저장된 값이 정렬된 형태
insert into emp(empno, ename, sal) values(111,'ssafy',3000);

/** View
	- Strored Query
    - 테이블과 달리 물리적인 저장공간을 가지지 않는다.
    - view에 select문으로 질의를 할 때마다 Stored Query가 수행된다.
    - 목적
		- 사용상의 편리성
		  복잡한 query를 view로 생성하고 단순 질의를 통해 결과를 조회할 수 있다
		- 수행속도 향상
          복작한 query를 성능 좋은 쿼리로 view를 생성한다.
		- 보안 관리를 목적
		  테이블의 일부 컬럼만 엑세스하게 한다.
		  보여주고 싶은 데이터만 보여준다
          
	형식]
    create [or replace] view 뷰이름
    as
    select문
*/

create or replace view Employee
as
select empno, ename, job, hiredate, sal , deptno, dname
from emp
left join dept
using (deptno);

select * from employee;

insert into emp(empno,ename,sal) values(2222,'ddd',2500);

update emp set sal = 3500 where deptno =30;
update emp set sal = (select * from (select avg(sal) from emp) avgsal)
where deptno = 10;
```

