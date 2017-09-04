### SQL 그래도 UNION이 필요한 경우

>UNION을 사용해야하는 경우

##### 
```SQL
// ----------------------------------- 1. UNION을 사용할 수 밖에 없는 경우 ----------------------------------- //
MERGE 대상이 되는 SELECT 구문들에서 사용하는 테이블이 다른 경우가 대표적이다.
쉽게 말하면 여러개의 테이블에서 검색한 결과를 머지하는 경우.

SELECT col_1
FROM   table_A
WHERE  col_2 = 'A'
UNION ALL
SELECT col_3
FROM   table_B
WHERE  col_4 = 'B'

CASE식을 사용할 수 없다는 것은 아닌데,
필요 없는 결합이 발생해서 성능적으로 악영향이 발생한다


// ------------------------------ 2. UNION을 사용하는 것이 성능적으로 좋은 경우 ------------------------------ //
집약에 조건 분기를 적용하는 또 하나의 패턴으로, 집약 결과에 조건 분기를 수행하는 경우

// 예제 테이블
   key    | name |   date_1   | flg_1 |   date_2   | flg_2 |   date_3   | flg_3
----------+------+------------+-------+------------+-------+------------+-------
 1        | a    | 2013-11-01 | T     |            |       |            |
 2        | b    |            |       | 2013-11-01 | T     |            |
 3        | c    |            |       | 2013-11-01 | F     |            |
 4        | d    |            |       | 2013-12-30 | T     |            |
 5        | e    |            |       |            |       | 2013-11-01 | T
 6        | f    |            |       |            |       | 2013-12-01 | F

// 출력 포맷
   key    | name |   date_1   | flg_1 |   date_2   | flg_2 |   date_3   | flg_3
----------+------+------------+-------+------------+-------+------------+-------
 1        | a    | 2013-11-01 | T     |            |       |            |
 2        | b    |            |       | 2013-11-01 | T     |            |
 5        | e    |            |       |            |       | 2013-11-01 | T

- UNION을 사용한 방법
SELECT key,
       name,
       date_1,
       flg_1,
       date_2,
       flg_2,
       date_3,
       flg_3
FROM   threeelements
WHERE  date_1 = '2013-11-01'
       AND flg_1 = 'T'
UNION
SELECT key,
       name,
       date_1,
       flg_1,
       date_2,
       flg_2,
       date_3,
       flg_3
FROM   threeelements
WHERE  date_2 = '2013-11-01'
       AND flg_2 = 'T'
UNION
SELECT key,
       name,
       date_1,
       flg_1,
       date_2,
       flg_2,
       date_3,
       flg_3
FROM   threeelements
WHERE  date_3 = '2013-11-01'
       AND flg_3 = 'T';

이 쿼리를 최적의 성능으로 수행하려면 다음과 같은 필드 조합에 인덱스가 필요하다.
CREATE INDEX IDX_1 ON ThreeElements (date_1, flg_1) ;
CREATE INDEX IDX_2 ON ThreeElements (date_2, flg_2) ;
CREATE INDEX IDX_3 ON ThreeElements (date_3, flg_3) ;

- OR을 사용한 방법

SELECT key, name,
       date_1, flg_1,
       date_2, flg_2,
       date_3, flg_3
　FROM ThreeElements
 WHERE (date_1 = '2013-11-01' AND flg_1 = 'T')
    OR (date_2 = '2013-11-01' AND flg_2 = 'T')
    OR (date_3 = '2013-11-01' AND flg_3 = 'T');

UNION과 OR의 성능 비교는 결국 3회의 인덱스 스캔 VS 1회의 테이블 풀 스캔중에서 어떤 것이 더 빠른지에 대한 문제
이는 테이블의 크기와 검색 조건에 따른 선택비율(레코드 히트율)에 따라 답이 달라진다
하지만 테이블이 크고, WHERE 조건으로 선택되는 레코드의 수가 충분히 작다면 UNION이 더 빠를 수도 있다.

- IN을 사용한 방법

SELECT key, name,
       date_1, flg_1,
       date_2, flg_2,
       date_3, flg_3
　FROM ThreeElements
 WHERE ('2013-11-01', 'T')
         IN ((date_1, flg_1),
             (date_2, flg_2),
             (date_3, flg_3));

IN의 매개변수로는 단순히 스칼라 뿐만 아니라, 이러게 (a, b, c)와 같은 값의 리스트(배열)을 입력도 가능
실행계획은 OR과 같다

- CASE식을 활용한 방법

SELECT key, name,
       date_1, flg_1,
       date_2, flg_2,
       date_3, flg_3
　FROM ThreeElements
 WHERE CASE WHEN date_1 = '2013-11-01' THEN flg_1
            WHEN date_2 = '2013-11-01' THEN flg_2
            WHEN date_3 = '2013-11-01' THEN flg_3
       ELSE NULL END = 'T';

```


