### Oracle 2. Aggregate Function

#### 데이터 분석을 이한 세 가지 함수를 정의
```{.javascript}
여러 행들의 그룹이 모여서 그룹당 단 하나의 결과를 돌려주는 다중행 함수중 집계함수의 특성은
- 여러 행들의 그룹이 모여서 단 하나의 결과를 돌려주는 함수이다.
- GROUP BY 절은 행들을 소그룹화 한다.
- SELECT, HAVING, ORDER BY 절에 사용할 수 있다.

count(*) - NULL 값을 포함한 행수를 출력
count(표현식) - 표현식의 값이 NULL값인 것을 제외한 행수 ex) count(height) height 컬럼에 null을 제외하고 count

검색절 where team_id in ('K09', K08') 
in - 표현식의 결과를 만족하는 모든 값을 출력

group by절을 사용하기 앞서 where절에서 계산되는 결과값을 줄이고 group by를 하는 것이 효율적이다.

EXTRACT - 추출함수 extract(month from hiredate(컬럼)) from emp; hiredate:1990-10-10 

DECODE와 CASE 함수는 SQL 문장에서 조건에 해당하는 값을 추출하고자 할 때 주로 사용한다

DECODE - 함수는 조건에 따라 데이터를 다른 값이나 컬럼값으로 추출 할 수 있다.
DECODE(VALUE, IF1, THEN1, IF2, THEN2...) 형태로 사용 할 수 있다.
- VALUE 값이 IF1일 경우에 THEN1 값을 반환하고,
  VALUE 값이 IF2일 경우에는 THEN2 값을 반환한다.- DECODE 함수 안에 DECODE함수를 중첩으로 사용 할 수 있다.

DECODE 함수는 4번째 인자를 지정하지 않으면 NULL이 default로 할당된다.
case문도 마찬가지...
SUM(CASE MONTH WHEN 1 THEN SAL END)  >>  SUM(CASE MONTH WHEN 1 THEN SAL ELSE 0 END) 불필요하게 ELSE절을 상수로 넣을 필요가 없다.
```
