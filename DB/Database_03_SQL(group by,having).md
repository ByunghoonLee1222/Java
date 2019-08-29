# SQL

#### GroupBy 절

* where 절은 행 하나하나에 대한 조건 판단
* having => 집계함수 결과(group by)에 대한 조건 판단
* **alias를 쓸수 있는곳은 order by 절에서만 가능**
* mySQL은 having 절에도 사용가능

```mysql
desc goods;
desc emp;
/*
	group by
    - 데이터를 지정한 컬럼을 기준으로 데이터를 종류 별로 분류하여
    데이터 그룹을 나눠서 group함수를 적용
    형식] group by 컬럼명, ...
*/
-- cno 별 등록된 상품 개수, 최고가, 최저가, 평균 가격 조회
select cno,count(*), max(price),min(price),avg(price)
from goods
group by cno;

-- 업무별 평균 급여 조회
select job, round(avg(sal))as avgSal
from emp
group by sal;

-- 제조사 별, 분류별 상품의 평균 가격을 조회
select maker, cno, round(avg(price)) as avgPrice
from goods
group by maker,cno
order by maker;

/*
having
	-group함수의 결과에 조건을 지정해서 데이터를 조회할 때 사용
    -형식] group by 컬럼, ...
		  having 조건
*/
-- 부서별 급여 평균이 2500이상인 부서를 조회
select deptno, round(avg(sal)) as avgSal
from emp
group by deptno
having avg(sal) >= 2500;

-- 분류별 가격 평균을 조회,
-- 가격 평균이 500000원 이상인 분류는 제외하고 조회한다
select cno, floor(avg(price)) as avgPrice
from goods
group by cno
having avg(price)<500000;

-- 급여가 1500이상인 사원들의 부서별 급여 평균을 조회
-- 단 급여 평균이 2000이상인 부서만 조회

select deptno, round(avg(sal)) as avgSal
from emp
where sal >=1500
group by deptno
having avg(sal)>=2000;

/*
rollup : group별 집계한 결과에 전체or중간 집계를 추가로 조회
형식 	  ] group by 컬럼명 with rollup;
oracle] group by rollup(컬럼명);
*/

-- 업무별 평균 급여 조회, 전체 급여 평균을 같이 조회
select ifnull(job,'total')as job, round(avg(sal)) avgSal
from emp
group by job with rollup;

-- 분류별 상품에 대한 가격 평균과, 전체 가격 평균을 조회
select if(grouping(cno)=1,'total',ifnull(cno,'미분류')) as cno, round(avg(price)) as avgPrice
from goods
group by cno with rollup;

/*
grouping(컬럼)
- rollup을 통해 나온 결과가 null이면 1,
  원래 값이 null이면 0을 추출하는 함수
*/

-- 부서별, 업무별 급여 평균을 조회 , 부서별 급여 평균, 전체 급여 평균을 조회
select if(grouping(deptno)=1,'전체급여 평균'
			,if(grouping(job)=1,'부서별 급여 평균',null))as 급여평균,deptno, job, round(avg(sal)) as avgSal
from emp
group by deptno, job with rollup
order by deptno,job desc;

insert into emp(empno,job, sal) values(1111,'ANALYST',3000);
-- 부서별, 업무별 급여 평균을 조회, 부서별 급여 평균, 전체 급여 평균을
-- Pivot 테이블로 조회
select if(grouping(deptno)=1,'전체통계',ifnull(deptno,'신입사원')) as deptno 
		,ifnull(round(avg(if(job = 'CLERK', sal, null))),0) as CLERK
        ,ifnull(round(avg(if(job = 'ANALYST', sal, null))),0) as ANALYST
        ,ifnull(round(avg(if(job = 'SALESMAN', sal, null))),0) as SALESMAN
        ,ifnull(round(avg(if(job = 'MANAGER', sal, null))),0) as MANAGER
        ,ifnull(round(avg(if(job = 'PRESIDENT', sal, null))),0) as PRESIDENT
        ,round(avg(sal))as avgSal
from emp
group by deptno with rollup
order by deptno;

```



