### SQL 자르기

>GROUP BY 구라는 것은 자르기와 집약 기능을 한꺼번에 수행하는 연산이다.
>자르기에 초점을 두고 살펴 보자.

##### 
```SQL
// ------------------------------------ 1. 자르기와 파티션 ------------------------------------ //

// 예제 테이블
   name   | age | height | weight
----------+-----+--------+-------
 Anderson |  30 |    188 |     90
 Adela    |  21 |    167 |     55
 Bates    |  87 |    158 |     48
 Becky    |  54 |    187 |     70
 Bill     |  39 |    177 |    120
 Chris    |  90 |    175 |     48
 Darwin   |  12 |    160 |     55
 Dawson   |  25 |    182 |     90
 Donald   |  30 |    176 |     53

// 첫문자로 알파벳마다 몇 명의 사람이 존재하는지 계산

SELECT SUBSTRING(name, 1, 1) AS label,
         COUNT(*)
　FROM Persons
 GROUP BY SUBSTRING(name, 1, 1);

- 파티션
이렇게 GROUP BY 구로 잘라 만든 하나하나의 부분 집합을 수학적으로 파티션 'partion'이라고 부른다.
파티션은 서로 중복되는 요소를 가지지 않는 부분 집합이다.

// 나이로 자르기
SELECT CASE WHEN age < 20 THEN '어린이'
            WHEN age BETWEEN 20 AND 69 THEN '성인'
            WHEN age >= 70 THEN '노인'
       ELSE NULL END AS age_class,
       COUNT(*)
　FROM Persons
 GROUP BY CASE WHEN age < 20 THEN '어린이'
               WHEN age BETWEEN 20 AND 69 THEN '성인'
               WHEN age >= 70 THEN '노인'
          ELSE NULL END;

```


