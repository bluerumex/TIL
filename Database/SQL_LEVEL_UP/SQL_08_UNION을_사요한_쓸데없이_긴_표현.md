### SQL UNION을 사용한 쓸데없이 긴 표현

>UNION은 성능적인 측면

##### 
```SQL
// ----------------------------------- 1. UNION을 사용한 조건 분기 ----------------------------------- //

// UNION 예제
// 20001년까지 세금이 포함되지 않는 가격과 2002년부터 세금이 포함된 가격을 필드로 표시
// items 테이블의 컬럼은 item_id, year, item_name, price_tax_ex(세전), price_tax_in(세후)

SELECT item_name, year, price tax_ex AS price
FROM items
WHERE year <= 2001
UNION
SELECT item_name, year, price_tax_in AS price
FROM items
WHERE year >= 2002;

조건이 배타적이르모 중복 레코드가 발행하지 않는다.

실행계획 확인방법
EXPLAIN
Query...

QUERY PLAN
----------------------------------------------------------
HashAggregate  (cost=36.86..39.92 rows=306 width=140)
Group Key: items.item_name, items.year, items.price_tax_ex
->  Append  (cost=0.00..34.56 rows=306 width=140)
     ->  Seq Scan on items  (cost=0.00..15.75 rows=153 width=140)
           Filter: (year <= 2001)
     ->  Seq Scan on items items_1  (cost=0.00..15.75 rows=153 width=140)
           Filter: (year >= 2002)

items 테이블에 2회 접근했다 그리고 그 때마다 TABLE ACCESS FULL이 발생하므로, 읽어드리는 비용도
테이블의 크기에 따라 선형으로 증가하게 된다.
물론 데이터 캐시에 테이블의 데이터가 있으면 어느 정도 그런 증상이 완화되겠지만,
테이브의 크기가 커지면 캐시 히트율이 낮아지므로 그런한 것도 기대하기 힘들어진다.

SQL의 격언
'조건 분기를 WHERE구로 하는 사람들은 초보자다. 잘하는 사람은 SELECT 구만으로 조건 분기를 한다'

SELECT item_name, year,
CASE WHEN year <= 2001 THEN price_tax_ex
	WHEN year >= 2002 THEN price_tax_in
END AS price
FROM items;

QUERY PLAN
----------------------------------------------------------
 Seq Scan on items  (cost=0.00..16.90 rows=460 width=140)

UNION을 사용한 분기보다 실행속도가 훨씬 빠르다(데이터 양이 많다고 생각하면 훨씬 효율적일 것임)

UNION과 CASE 쿼리의 구문적인 관점에서 비교
UNION을 사용한 분기는 SELECT '구문'을 기본 단위로 분기하고 있다. 구문을 기본 단위로 사용하고 있다는
점에서 아직 절차 지향형의 발상을 벗어나지 못한 방법이라고 말할 수 있다.
반면 CASE 식을 사용한 분기는 문자 그대로 '식'을 바탕으로 하는 사고라 할수 있다
```


