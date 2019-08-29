# SQL 

* **SELECT**

```mysql

-- 데이터베이스에 선언된 테이블 조회
show tables

-- TABLE 구조 조회 desc 테이블명
desc goods;

-- goods테이블의 모든 데이터 조회
select *
from goods;		-- where 조건이 없으면 모든 행 조회

-- 모든 상품의 상품번호, 상품이름, 가격 조회
select gno, brand, price
from goods;

-- 칼럼에 연산이나 함수 적용
-- 모든 상품의 상품번호, 상품이름, 가격, 10%인상된 가격 조회
select gno, brand, price, price * 1.1 as IncPrice
from goods;

/*
where 절 : 조건에 맞는 행만 추출
조건 연산자
같음 = , 다름 != <>, >, <, >=, <=
논리 and or
*/

-- 가격이 5000원 이상인 상품들에 대한 상품번호, 상품명, 가격을 조회
select gno, brand, price
from goods
where price >=5000;

-- 10번 분류에 속한 상품들의 모든 정보 조회
select *
from goods
where cno = 10;

-- 10번 분류에 속하지 않은 상품들의 모든 정보 조회
select *
from goods
where cno <> 10;

/*
	is null : 값이 null인지 비교
    is not null : 값이 null이 아닌지 비교
*/
-- 특정 분류에 속하지 않은 상품 정보 조회
select *
from goods
where cno is null;

-- 분류 번호가 있는 상품 정보 조회
select *
from goods
where cno is not null;

-- distinct 중복 값 제거
-- 상품이 있는 분류 번호 조회

select * from category;
select distinct cno from goods;
select cno from goods;

-- 가격이 5000원 이상 15000원 이하인 제품들을 조회

select *
from goods
where price >=5000 and price<=15000;

/* between 범위 검사
   형식] 컬럼명 between 작은값 and 큰값
*/
select *
from goods
where price between 5000 and 15000;
-- 큰값 and 작은값 => 조회 안됨
select *
from goods
where price between 15000 and 5000;

-- 분류 번호가 10이거나 20번인 상품들을 조회
select *
from goods
where cno = '10' or cno = '20';
-- 다른 데이터베이스는 문자 ' ' 와 숫자를 구분해서 써야한다
/*
 in: 열거형 데이터로 조회 할 때
	 주어진 데이터 중 하나라도 일치하면 조회된다
     형식] 컬럼명 in (값, 값, ...)
*/
select *
from goods
where cno in ('10','20');

-- 분류번호가 10번이 아니고 20번이 아닌 상품들 조회
select *
from goods
where cno != '10' and cno <> '20';

-- not in(~) : 주어진 열거형 데이터와 모두 일치 하지 않아야 조회
select *
from goods
where cno not in ('10','20');

/*
	- 제공된 조건이 포함되어 있는 데이터를 조회
    - 대체 문자
    % : 문자 길이 상관 없이 대체
    ex) '김_' : 성이 김씨이고 이름이 2자인 사람 조회
		'김%' : 성이 김씨로 시작하는 사람 조회
        '%김%': 김이 들어가는 사람 조회
*/

-- 삼성이라는 글자가 들어간 제조사의 모든 제품을 조회
select *
from goods
where maker like '%삼성%';

-- 모든 마우스 제품을 조회
select *
from goods
where brand like '%마우스%';

/*
case ~ when ~ then
- when에 저장된 조건이 참이면 then에 지정한 연산식이나 데이터가 처리
- ANSI Query(모든 데이터 베이스에서 사용하는 표준 쿼리)
- 형식]
	case
		when 조건 then 조건이 true일때 수행할 값, 연산식
        when ...
        else 주어진 조건이 모두 아닌 경우 수행될 값, 연산식
	end
        
*/
/*
	상품 번호, 이름 , 가격, 분류 번호, 분류 명
    분류 번호가 10번인 경우 음식
			 20번인 경우 전자 제품
             30번인 경우 서적
             40번인 경우 가구
             분류번호가 없는 경우 미분류로 표시
*/
select gno, brand, price, cno 
, case when cno = '10' then '음식'
	   when cno = '20' then '전자 제품'
	   when cno = '30' then '서적'
	   when cno = '40' then '가구'
       else '미분류'
  end as 분류명
from goods;

/*
	상품번호(gno), 상품명(brand), 인상적 가격(price), 인상 후 가격을 조회(IncPrice)
    가격 인상은 다음과 같다
    가격이 10000원 미만 이면 15%를 인상
    가격이 10000원 이상 200000원 이하이면 10%를 인상
    가격이 200000원을 초과하면 5%를 인상
*/
select gno, brand, price
	,case when price <10000 then price*1.15
		  when price <=200000 then price*1.10
          else price*1.05
	 end as IncPrice
from goods;

/*
	order by : 데이터 정렬
		- 지정한 컬럼의 데이터를 기준으로 정렬
        - 기본적으로 오름 차순으로 정렬한다.
        - asc : 오름 차순 desc : 내림차순
*/

-- 상품의 모든 데이터를 조회, 가격을 기준으로 오름차순 정렬
select *
from goods
order by price; -- 기본이 오름차순이므로 asc는 생략해도 됨

-- 상품의 모든 데이터를 조회, 가격을 기준으로 내림 차순 정렬
select *
from goods
order by price desc;

-- 분류 번호를 기준으로 내림차순 정렬, 같은 분류 내에서는 제품명을 기준으로 오름차순 정렬
select *
from goods
order by cno desc, brand;
/*
	상품번호(gno), 상품명(brand), 인상적 가격(price), 인상 후 가격을 조회(IncPrice)
    가격 인상은 다음과 같다
    가격이 10000원 미만 이면 15%를 인상
    가격이 10000원 이상 200000원 이하이면 10%를 인상
    가격이 200000원을 초과하면 5%를 인상
    인상된 가격을 기준으로 오름차순 정렬
*/
select gno, brand, price
	,case when price <10000 then price*1.15
		  when price <=200000 then price*1.10
          else price*1.05
	 end as IncPrice
from goods
order by IncPrice;

-- desc dual;
-- select * from dual;
/*
	dual 테이블
    - 한개의 열과 한개의 행으로 구성된 Dummy 테이블
    
    - 연산이나 함수를 수행한 결과를 조회할려면 select문을 통해 조회해야 한다
    - 간단한 연산이나 함수를 조회할 때 select문을 사용하면 from의 테이블수만큼
	  처리한 결과가 나온다.
	- 간단한 연산이나 함수를 조회할 때 dual 테이블을 통해 조회하면 빠르다.
*/
select 10*100 from goods;
select 10*100 from dual;
```

