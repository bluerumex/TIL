### SQL 집계와 조건 분기

>다양한 집계와 조건 분기 방법

##### 
```SQL
// ----------------------------------- 1. 집계 대상으로 조건 분기 ----------------------------------- //
// 예제 테이블
 prefecture | sex | pop
------------+-----+----
 성남       | 1   |  60
 성남       | 2   |  40
 수원       | 1   |  90
 수원       | 2   | 100
 광명       | 1   | 100
 광명       | 2   |  50
 일산       | 1   | 100
 일산       | 2   | 100
 용인       | 1   |  20
 용인       | 2   | 200

// 원하는 출력 결과
 prefecture | man | woman
------------+-----+-------
 광명       | 100 |    50
 성남       |  60 |    40
 수원       |  90 |   100
 용인       |  20 |   200
 일산       | 100 |   100

- UNION을 사용한 방법

이 문제를 절차지향적인 사고방식을 가진다면, 일단 남성의 인구를 지역별로 구하고,
여성의 인구를 지역별로 구한 뒤 머지(MERGE)하는 방법을 생각할 것이다.

SELECT prefecture,
       Sum(pop_man)   AS man,
       Sum(pop_woman) AS woman
FROM   (SELECT prefecture,
               pop  AS pop_man,
               NULL AS pop_woman
        FROM   population
        WHERE  sex = '1'
        UNION
        SELECT prefecture,
               NULL AS pop_man,
               pop  AS pop_woman
        FROM   population
        WHERE  sex = '2') z
GROUP  BY prefecture;

원하는 결과를 도출할 수 있지만 이 쿼리의 가장 큰 문제는 WHERE구에서 sex 필드로 분기를 하고,
결과를 UNION으로 머지한다는 절차 지향적인 구성에 있다.

집계의 조건 분기도 CASE식을 활용
실행계획 또한 더 간단하진다.
풀스캔이 1회로 감소

SELECT prefecture,
       Sum(CASE
             WHEN sex = '1' THEN pop
             ELSE 0
           END) AS man,
       Sum(CASE
             WHEN sex = '2' THEN pop
             ELSE 0
           END) AS woman
FROM   population
GROUP  BY prefecture;

// ----------------------------------- 2. 집약 결과로 조건 분기 ----------------------------------- //
집약에 조건 분기를 적용하는 또 하나의 패턴으로, 집약 결과에 조건 분기를 수행하는 경우
// 예제 테이블
 emp_id | team_id |     emp_name     |         team
--------+---------+------------------+----------------------
 201    |       1 | Joe              | 상품기획
 201    |       2 | Joe              | 개발
 201    |       3 | Joe              | 영업
 202    |       2 | Jim              | 개발
 203    |       3 | Carl             | 영업
 204    |       1 | Bree             | 상품기획
 204    |       2 | Bree             | 개발
 204    |       3 | Bree             | 영업
 204    |       4 | Bree             | 관리
 205    |       1 | Kim              | 상품기획
 205    |       2 | Kim              | 개발


// 원하는 출력 결과
     emp_name     |        team
------------------+--------------------
 Jim              | 개발
 Joe              | 3개 이상을 겸무
 Bree             | 3개 이상을 겸무
 Kim              | 2개를 겸무
 Carl             | 영업

- UNION으로 조건 분기
SELECT emp_name,
       Max(team) AS team
FROM   employees
GROUP  BY emp_name
HAVING Count(*) = 1
UNION
SELECT emp_name,
       '2개를 겸무' AS team
FROM   employees
GROUP  BY emp_name
HAVING Count(*) = 2
UNION
SELECT emp_name,
       '3개 이상을 겸무' AS team
FROM   employees
GROUP  BY emp_name
HAVING Count(*) >= 3;

- CASE 식을 사용한 조건 분기
SELECT emp_name,
       CASE
         WHEN Count(*) = 1 THEN Max(team)
         WHEN Count(*) = 2 THEN '2개를 겸무'
         WHEN Count(*) >= 2 THEN '2개 이상을 겸무'
       END AS team
FROM   employees
GROUP  BY emp_name;



```


