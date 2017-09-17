### SQL 서브쿼리가 일으키는 폐해

>서브쿼리란 SQL내부에서 작성되는 일시적인 테이블이다(이를 영속화 한것은 VIEW)
>기능점관점에서 테이블과 서브쿼리는 차이가 없지만, 비기능적인 관점(특히 성능)에서 보면
>큰 차이가 존재한다

##### 
```SQL
// ------------------------------------ 1. 서브쿼리의 문제점 ----------------------------------------- //

서브쿼리의 성능적 문제는 결과적으로 서브쿼리가 실체적인 데이터를 저장하고 있지 않다는 점에서 기인

- 연산비용 추가
	실제적인 데이터를 저장하고 있지 않다는 것은 서브쿼리에 접근할 때마다 SELECT 구문을 실행해서
    데이터르 만들어야 한다는 뜻이다.
    SELECT 구문이 복잡할 수록 실행 비용은 더 높아진다.

- 데이터 I/O 비용 발생
	연산 결과는 어딘가에 저장하기 위해 써두어야 한다. 메모리 용량이 충분하다면 이러한 오버헤드가
    적지만 데이터양이 큰 경우 DBMS 저장소에 있는 파일에 결과를 쓸 때도 있다.
    TEMP 탈락 현상의 일종으로 이렇게 되면 저장소 성능에 따라 접근 속도가 급격히 떨어진다.

- 최적화를 받을 수 없다
	서브쿼리로 만들어지는 데이터는 구조적으로 테이블과 차이는 없다.
    하지만 명시적인 제약 또는 인덱스가 작성되어 있는 테이블과 달리, 서브쿼리에는 그런 메타 정보가 없다.
    옵티마이저가 쿼리를 해석하기 위해 필요한 정보를 서브쿼리에서는 얻을 수 없다.
    (현재 대안으로 VIEW MERGING이라는 것이 있다)



// ------------------------------------ 2. 서브쿼리 의존증 ------------------------------------ //

// 예제 테이블
순번(SEQ) 피드는 구입 시기가 오래될수록 작은 값을 갖는다.

 cust_id | seq | price
---------+-----+-------
 A       |   1 |   500
 A       |   2 |  1000
 A       |   3 |   700
 B       |   5 |   100
 B       |   6 |  5000
 B       |   7 |   300
 B       |   9 |   200
 B       |  12 |  1000
 C       |  10 |   600
 C       |  20 |   100
 C       |  45 |   200
 C       |  70 |    50
 D       |   3 |  2000

// 출력 포맷
 cust_id | seq | price
---------+-----+-------
 D       |   3 |  2000
 B       |   5 |   100
 C       |  10 |   600
 A       |   1 |   500

- 서브쿼리를 사용한 방법
SELECT R1.cust_id, R1.seq, R1.price
　FROM Receipts R1
         INNER JOIN
           (SELECT cust_id, MIN(seq) AS min_seq
              FROM Receipts
             GROUP BY cust_id) R2
    ON R1.cust_id = R2.cust_id
　 AND R1.seq = R2.min_seq;

위 쿼리가 성능이 나쁜 이유
1. 서브쿼리는 대부분 일시적인 영역(메모리 또는 디스크)에 확보되므로 오버헤드가 생김
2. 서브쿼리는 인덱스 또는 제약 정보를 가지지 않기 때문에 최적화되지 못한다.
3. 이 쿼리는 결합을 필요로 하기 때문에 비용이 높고 실행 계획 변동 리스크가 발생한다.
4. 테이블에 스캔이 두번 필요하다.

- 상관서브쿼리는 답이 될 수 없다
SELECT cust_id, seq, price
　FROM Receipts R1
 WHERE seq = (SELECT MIN(seq)
                FROM Receipts R2
               WHERE R1.cust_id = R2.cust_id);

상관서브쿼리를 사용하더라도 테이블 접근이 두 번 발생한다.(실행계획 참조)

- 윈도우 함수로 결합을 제거
일단 개선해야 하는 부분은 Receipts 테이블에 대한 접근을 1회로 줄여야한다.
SQL 튜닝에서 가장 중요한 부분이 바로 I/O를 줄이는 것
접근을 줄이려면 윈도우 함수 ROW_NUMBER를 이용한다

SELECT cust_id, seq, price
　FROM (SELECT cust_id, seq, price,
               ROW_NUMBER()
                 OVER (PARTITION BY cust_id
                           ORDER BY seq) AS row_seq
          FROM Receipts ) WORK
 WHERE WORK.row_seq = 1;

FROM절의 결과
cust_id | seq | price | row_seq
--------+-----+-------+---------
A       |   1 |   500 |       1
A       |   2 |  1000 |       2
A       |   3 |   700 |       3
B       |   5 |   100 |       1
B       |   6 |  5000 |       2
B       |   7 |   300 |       3
B       |   9 |   200 |       4
B       |  12 |  1000 |       5
C       |  10 |   600 |       1
C       |  20 |   100 |       2
C       |  45 |   200 |       3
C       |  70 |    50 |       4
D       |   3 |  2000 |       1

실행 계획
Receipts 테이블에 대한 접근이 1회로 감소했다.
물론 윈도우 함수에서 정렬을 사용하는 것이 추가되기는 했지만 지금까지 살펴본 다른 코드들에서도
MIN 함수를 사용했었으므로 이런 부분에서 큰 비용 차이가 발생하지는 않을 것이다.


// --------------------------------- 3. 장기적 관점에서의 리스크 관리 --------------------------------- //
결합을 사용한 쿼리는 2개의 불안정 요소가 있다.
1. 결합 알고리즘의 변동 리스크
2. 환경 요인에 의한 지연 리스크(인덱스, 메모리, 매개변수 등)

- 알고리즘 변동 리스크
결합 알고리즘에는 크게 Nested Loops, Sort Merge, Hash라는 세가지 종류가 있다.
이들 중 어떤 것을 선택할지는 테이블의 크기 등을 고려해 옵티마이저가 자동으로 결장한다.

대략적으로 크기가 작은 테이블이 포함된 경우 Nested Loops가 선택되기 쉽고,
큰 테이블들을 결합하는 경우 Sort Merge, Hash가 선택되기 쉽다.

따라서 처음에는 테이블의 레코드 수가 적어 Nested Loop를 사용하다가도,
시스템을 운용하면서 레코드가 늘어나, 어느 순간 역치를 넘으면 실행 계획 변동이 생기게 된다.
이때 성능에 큰 변화가 일어나는데 좋아지는 경우도 있지만 오히려 악화되는 경우도 많게된다.

데이터양이 많아지면서 Sort Merge 또는 Hash에 필요한 메모리가 부족해지면서 저장소를 사용하게된다
(TEMP 탈락 현상)

- 환경 요인에 의한 지연 리스크
Nested Loops의 내부 테이블 결합 키에 인덱스가 존재하면 성능이 크게 개선된다.
또한 Sort Merge 또는 Hash가 선택되어 TEMP 탈락이 발생하는 경우 작업 메모리를 늘려주면
성능을 개선할 수 있다.
하지만 메모리 튜닝은 한정된 리소스 내부에서 트레이드 오프를 발생시킨다.

// --------------------------------- 4. 서브쿼리 의존중 - 응용편 --------------------------------- //

Receipts 테이블의 최소값과 최대값의 차이를 구하는 필드

 cust_id | diff
---------+------
 D       |    0
 B       | -900
 C       |  550
 A       | -200

SELECT TMP_MIN.cust_id,
       TMP_MIN.price - TMP_MAX.price AS diff
　FROM (SELECT R1.cust_id, R1.seq, R1.price
          FROM Receipts R1
                 INNER JOIN
                  (SELECT cust_id, MIN(seq) AS min_seq
                     FROM Receipts
                    GROUP BY cust_id) R2
            ON R1.cust_id = R2.cust_id
           AND R1.seq = R2.min_seq) TMP_MIN
       INNER JOIN
       (SELECT R3.cust_id, R3.seq, R3.price
          FROM Receipts R3
                 INNER JOIN
                  (SELECT cust_id, MAX(seq) AS min_seq
                     FROM Receipts
                    GROUP BY cust_id) R4
            ON R3.cust_id = R4.cust_id
           AND R3.seq = R4.min_seq) TMP_MAX
    ON TMP_MIN.cust_id = TMP_MAX.cust_id;

- 다시 서브쿼리 의존중
서브쿼리를 사용해 구하는 방법
최솟값의 집합을 찾고, 최댓값의 집합을 찾은 뒤 고객 ID를 키로 결합
상기 쿼리는 코드가 굉장히 길고, 가독성도 좋지 않다.
그리고 서브쿼리의 계층이 굉장히 깊어서 어떤 부분이 서브쿼리인지 확인하는것도 힘들다
이전 쿼리를 두 번 붙여 넣기 한것이라 테이블에 대한 접근도 2배가 되어 4번이 이루어진다
따라서 성능이 좋은 쿼리라 할 수가 없다.

- 레코드 간 비교에서도 결합은 불필요
SELECT cust_id,
       SUM(CASE WHEN min_seq = 1 THEN price ELSE 0 END)
         - SUM(CASE WHEN max_seq = 1 THEN price ELSE 0 END) AS diff
　FROM (SELECT cust_id, price,
               ROW_NUMBER() OVER (PARTITION BY cust_id
                                      ORDER BY seq) AS min_seq,
               ROW_NUMBER() OVER (PARTITION BY cust_id
                                      ORDER BY seq DESC) AS max_seq
          FROM Receipts ) WORK
 WHERE WORK.min_seq = 1
    OR WORK.max_seq = 1
 GROUP BY cust_id;

이렇게 하면 서브쿼리는 WORK 하느뿐이다. 그리고 결합도 발생하지 않는다.
Receipts 테이블 스캔 횟수가 1회로 감소
윈도우 함수로 정렬이 2회 발생하지만 결합을 반복하는 것보다 저렴하고 실행계획의 안정성도 확보할 수
있기 때문에 더 좋은 쿼리라 할 수 있다.
```


