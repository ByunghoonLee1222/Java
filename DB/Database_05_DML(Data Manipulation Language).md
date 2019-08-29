# DML(Data Manipulation Language)

* record lock
  * 같은 서버 사용시 commit 하지 않으면 대기 상태



* **Insert** 
* **Update** 
* **Delete** 

```mysql
/*데이터 
insert into 테이블명(컬럼명,...)
- 지정한 컬럼 순서대로 데이터를 테이블에 추가
insert into values(값,...)
- 테이블 구조에 설정된 모든 컬럼에 구조에 지정된 순서대로 테이터를 추가

*/

insert into goods(brand, price,maker,cno)
values ( '핸디형선풍기',22000,'카카오프랜즈',20);
insert into member(id, password,email,phone,address)
values('ssafy','1111','ssafy@malcam.com','010','강남구');
insert into member(id, password,email,phone,address)
values('jaen','1111','jaen@malcam.com','010','서초구');
select * from goods;

/*
orders테이블의 id컬럼이 member 테이블의 id컬럼을 참조
member테이블 id에 kkk가 없는 경우 데이터 추가나 update하면 error발생 
insert into orders(id,gno,quantitiy)
values('kkk',1,10);
*/

savepoint insertGoods;

/*
delelte문
- 테이블에서 데이터 삭제
- 전체 데이터 삭제
  delete from 테이블;
- 조건에 맞는 데이터만 삭제
  delete from 테이블 where 조건;
*/

delete from goods;
select * from goods;
rollback to insertGoods; -- insertGoods까지 취소 delete문이 취소됨

delete from emp where empno=1111;

commit;

/*
	update : 데이터 수정
    - 전체 데이터 수정
    update 테이블명 set 컬럼명 = 값, ...;
    
    -조건에 맞는 데이터만 수정
    update 테이블명 set 컬럼명 = 값, ...where 조건;
*/
update emp set sal = 30000;
select * from emp;
rollback;
update emp set sal = 4500 where empno =1111;
commit;

/*
index
 - select문의 성능을 높이기 위해서 index만든다
 형식] create index 인덱스명 on 테이블명(컬럼명,..);
*/

-- goods 테이블의 상품명에 indexing
create index idx_goods_brand on goods(brand);


```

