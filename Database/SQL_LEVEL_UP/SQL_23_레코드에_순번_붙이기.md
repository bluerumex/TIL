### SQL 레코드에 순번 붙이기

>레코드에 순서를 순번을 붙이는 방법에 대해 알아보자

##### 
```SQL
// ------------------------------------ 1. 기본키가 한 개의 필드일 경우 ----------------------------------------- //

//체중 테이블
 student_id | weight
------------+--------
 A100       |     50
 A101       |     55
 A124       |     55
 B343       |     60
 B346       |     72
 C563       |     72
 C345       |     72

- 윈도우 함수를 사용
학생 ID를 오름차순으로 순번을 붙여보자.
ROW_NUMBER 함수를 사용할 수 있는 환경이라며 간단하게 구현할 수 있다.

 student_id | seq
------------+-----
 A100       |   1
 A101       |   2
 A124       |   3
 B343       |   4
 B346       |   5
 C345       |   6
 C563       |   7

SELECT student_id,
       ROW_NUMBER() OVER (ORDER BY student_id) AS seq
  FROM Weights;

- 상관 서브쿼리를 사용
MySQL 처럼 ROW_NUMBER 함수를 사용할 수 없는 환경에서는 상관 서브쿼리를 사용해야 한다.

SELECT student_id,
       (SELECT COUNT(*)
          FROM Weights W2
         WHERE W2.student_id <= W1.student_id) AS seq
　FROM Weights W1
```


