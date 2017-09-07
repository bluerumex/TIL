### SQL 집약

>레코드 단위가 아닌 '집합' 단위로 처리하는 집합 지향(set-oriented) 사고로 코드를 작성해보자.
>SQL에는 집약 함수(aggregate function)라고 하는 집약함수가 있다
>COUNT, SUM, AVG, MAX, MIN

##### 
```SQL
// ------------------------------- 1. 여러 개의 레코드를 한 개의 레코드로 집약 ------------------------------- //

// 예제 테이블
 id  | data_type | data_1 | data_2 | data_3 | data_4 | data_5 | data_6
-----+-----------+--------+--------+--------+--------+--------+--------
Jim  | A         |    100 |     10 |     34 |    346 |     54 |
Jim  | B         |     45 |      2 |    167 |     77 |     90 |    157
Jim  | C         |        |      3 |    687 |   1355 |    324 |    457
Ken  | A         |     78 |      5 |    724 |    457 |        |      1
Ken  | B         |    123 |     12 |    178 |    346 |     85 |    235
Ken  | C         |     45 |        |     23 |     46 |    687 |     33
Beth | A         |     75 |      0 |    190 |     25 |    356 |
Beth | B         |    435 |      0 |    183 |        |      4 |    325
Beth | C         |     96 |    128 |        |      0 |      0 |     12

A data_type = data_1, data_2
B data_type = data_3, data_4, data_5
C data_type = data_6


SELECT id,
       CASE WHEN data_type = 'A' THEN data_1 ELSE NULL END AS data_1,
       CASE WHEN data_type = 'A' THEN data_2 ELSE NULL END AS data_2,
       CASE WHEN data_type = 'B' THEN data_3 ELSE NULL END AS data_3,
       CASE WHEN data_type = 'B' THEN data_4 ELSE NULL END AS data_4,
       CASE WHEN data_type = 'B' THEN data_5 ELSE NULL END AS data_5,
       CASE WHEN data_type = 'C' THEN data_6 ELSE NULL END AS data_6
　FROM NonAggTbl
 GROUP BY id;

// 이 쿼리는 문법 오류가 발생한다
GROUP BY 구로 집약했을대 SELECT 구에 입력할 수 있는 것은 다음과 같은 세가지 뿐이다.
1) 상수
2) GROUP BY 구에서 사용한 집약키
3) 집약함수

따라서 아래와 같이 수정해야 된다

SELECT id,
       MAX(CASE WHEN data_type = 'A' THEN data_1 ELSE NULL END) AS data_1,
       MAX(CASE WHEN data_type = 'A' THEN data_2 ELSE NULL END) AS data_2,
       MAX(CASE WHEN data_type = 'B' THEN data_3 ELSE NULL END) AS data_3,
       MAX(CASE WHEN data_type = 'B' THEN data_4 ELSE NULL END) AS data_4,
       MAX(CASE WHEN data_type = 'B' THEN data_5 ELSE NULL END) AS data_5,
       MAX(CASE WHEN data_type = 'C' THEN data_6 ELSE NULL END) AS data_6
　FROM NonAggTbl
 GROUP BY id;

                            QUERY PLAN
-------------------------------------------------------------------
HashAggregate  (cost=34.22..36.22 rows=200 width=106)
  Group Key: id
  ->  Seq Scan on nonaggtbl  (cost=0.00..15.70 rows=570 width=114)

GROUP BY의 집약 조작에 'Hash' 알고리즘을 사용하고 있다.(ORACLE 또한)
집약할때 정렬 알고리즘을 사용하기도 하지만 해시를 사용하는 경우가 많다.
GROUP BY 구에 지정되어 있는 필드를 해시 함수를 사용해 해시키로 변환하고,
같은 해시 키를 가진 그룹을 모아 집약한다.

해시의 성질상 GROUP BY의 유일성이 높으면 더 효율적으로 작동한다

GROUP BY와 관련된 성능 주의점
정렬과 해시 모두 메모리를 많이 사용하므로, 충분한 해시용(또는 정렬용) 워킹 메모리가 확보되지 않으면
스왑이 발생 따라서 저장소 위의 파일이 사용되면서 굉장히 느려진다
ORACLE 에서는 정렬 또는 해시를 위해 PGA라는메모리 영역을 사용하는데,
이때 PGA 크기가 집약 대상 데이터양에 비해 부족하면, 임시 영역(저장소)를 사용해 부족한 만큼 채운다.
극단적으로 성능 저하가 발생

메모리와 저장소(일반적으로 디스크)의 접근 속도 차이가 굉장히 많이 나기 때문이다.


// --------------------------------------- 2. 합쳐서 하나 --------------------------------------- //

// 예제 테이블
 product_id | low_age | high_age | price
------------+---------+----------+-------
 제품1      |       0 |       50 |  2000
 제품1      |      51 |      100 |  3000
 제품2      |       0 |      100 |  4200
 제품3      |       0 |       20 |   500
 제품3      |      31 |       70 |   800
 제품3      |      71 |      100 |  1000
 제품4      |       0 |       99 |  8900

0세에서 100세까지 모든 연령이 가지고 놀 수 있는 제품을 구하는 쿼리 작성

SELECT product_id
　FROM PriceByAge
 GROUP BY product_id
HAVING SUM(high_age - low_age + 1) = 101;

각 범위에 있는 상수 개수를 모두 더한 합계가 101인 제품을 구하면 된다.

// 예제 테이블
 room_nbr | start_date |  end_date
----------+------------+-----------
      101 | 2008-02-01 | 2008-02-06
      101 | 2008-02-06 | 2008-02-08
      101 | 2008-02-10 | 2008-02-13
      202 | 2008-02-05 | 2008-02-08
      202 | 2008-02-08 | 2008-02-11
      202 | 2008-02-11 | 2008-02-12
      303 | 2008-02-03 | 2008-02-17

숙박한 날이 10일 이상인 방을 선택

SELECT room_nbr,
       SUM(end_date - start_date) AS working_days
　FROM HotelRooms
 GROUP BY room_nbr
HAVING SUM(end_date - start_date) >= 10;
```


