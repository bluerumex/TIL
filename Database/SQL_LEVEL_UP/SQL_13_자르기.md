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

- BMI로 자르기

   name   |       bmi        |  분류
----------+------------------+-------
 Anderson | 25.4640108646446 | 과체중
 Adela    | 19.7210369679802 | 정상
 Bates    | 19.2276878705336 | 정상
 Becky    | 20.0177299894192 | 정상
 Bill     | 38.3031695872833 | 과체중
 Chris    | 15.6734693877551 | 저체중
 Darwin   |        21.484375 | 정상
 Dawson   |  27.170631566236 | 과체중
 Donald   |  17.110020661157 | 저체중

BMI 값을 구하는 쿼리
SELECT NAME, weight / Power(height / 100, 2) AS BMI,
       CASE WHEN weight / Power(height / 100, 2) < 18.5 THEN '저체중'
            WHEN 18.5 <= weight / Power(height / 100, 2)
                 AND weight / Power(height / 100, 2) < 25 THEN '정상'
            WHEN weight / Power(height / 100, 2) >= 25 THEN '과체중'
       ELSE NULL END AS 분류
FROM   persons;


result | count
-------+-------
정상   |     4
저체중 |     2
과체중 |     3


SELECT CASE WHEN weight / POWER(height /100, 2) < 18.5 THEN '저체중'
            WHEN 18.5 <= weight / POWER(height /100, 2)
                   AND weight / POWER(height /100, 2) < 25 THEN '정상'
            WHEN 25 <= weight / POWER(height /100, 2) THEN '과체중'
            ELSE NULL END AS bmi,
            COUNT(*)
　FROM Persons
 GROUP BY CASE WHEN weight / POWER(height /100, 2) < 18.5 THEN '저체중'
               WHEN 18.5 <= weight / POWER(height /100, 2)
                   AND weight / POWER(height /100, 2) < 25 THEN '정상'
               WHEN 25 <= weight / POWER(height /100, 2) THEN '과체중'
               ELSE NULL END;

이처럼 GROUP BY 구에는 필드 이름만 적을 수 있는게 아니라 이렇게 복잡한 수식을 기준으로도 자를 수 있다.


// ------------------------------- 2. PARTITYON BY 구를 사용한 자르기 ------------------------------------ //

GROUP BY 구에서 집약 기능을 제외하고 자르기 기능만 남긴것이 윈도우 함수의 PARTITION BY 구이다.

// 출력 포맷
  name   | age | age_class | age_rank_in_class
---------+-----+-----------+------------------
Bates    |  87 | 노인      |                 1
Chris    |  90 | 노인      |                 2
Adela    |  21 | 성인      |                 1
Dawson   |  25 | 성인      |                 2
Anderson |  30 | 성인      |                 3
Donald   |  30 | 성인      |                 3
Bill     |  39 | 성인      |                 5
Becky    |  54 | 성인      |                 6
Darwin   |  12 | 어린이    |                 1

같은 연령 등급 (어린이, 성인, 노인)에서 어린 순서로 순위를 매기는 코드
PARTITION BY 구는 GROUP BY 구와 달리 집약 기능이 없으므로 원래 PERSON 테이블의 레코드가
모두 원래 형태로 나온다는 것을 염두해 두자.

SELECT name,
       age,
       CASE WHEN age < 20 THEN '어린이'
            WHEN age BETWEEN 20 AND 69 THEN '성인'
            WHEN age >= 70 THEN '노인'
       ELSE NULL END AS age_class,
       RANK() OVER(PARTITION BY CASE WHEN age < 20 THEN '어린이'
                                     WHEN age BETWEEN 20 AND 69 THEN '성인'
                                     WHEN age >= 70 THEN '노인'
                                ELSE NULL END
                       ORDER BY age) AS age_rank_in_class
　FROM Persons
 ORDER BY age_class, age_rank_in_class;

- CH12, CH13, CH14 요약
1. GROUP BY 구 또는 윈동 함수의 PARTITION BY 구는 집합을 자를 때 사용
2. GROUP BY 구 또는 윈도우 함수는 내부적으로 해시 또는 정렬 처리를 실행
3. 해시 또는 정렬은 메모리를 많이 사용해 만약 메모리가 부족하면 저장소를 사용해 성능 이슈 발생
4. GROUP BY 구 또는 윈도우 함수와 CASE식을 사용해 다양한 것을 표현할 수 있다.
```


