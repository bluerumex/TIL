#6 kyu
##SQL Basics: Simple NULL handling

```
Description:

For this challenge you need to create a SELECT statement, this select statement must have NULL handling, 
using COALESCE and NULLIF.

If no name is specified you must replace with [product name not found]

If no card_name is specified you must replace with [card name not found]

If no price is specified you must throw away the record, 
you must also filter the dataset by prices greater than 50.

eusales table schema

id
name
price
card_name
card_number
transaction_date
resultant table schema

id
name
price (greater than 50.00)
card_name
card_number
transaction_date

```

###Solution
```{.sql}
SELECT id,
       COALESCE (NULLIF(name, ''), '[product name not found]') AS name,
       price,
       COALESCE (NULLIF(card_name, ''), '[card name not found]') AS card_name,
       card_number,
       transaction_date
  FROM eusales
 WHERE price >= 50;

```

#####함수정리

- NULLIF(exp1, exp2) <br>
  exp1값과 exp2값이 동일하면 NULL을 그렇지 않으면 exp1을 반환
  CASE WHEN expr1 = expr2 THEN NULL ELSE expr1 END 
   
- COALESCE(expr1,expr2,expr3,…) <br>
  expr1이 NULL이 아니면 expr1값을 그렇지 않으면 COALESCE(expr2,expr3,…)값을 반환.
  NVL 함수와 비슷하다.

- NVL2 <br>
  NVL함수에 DECODE 함수의 개념을 합친 함수.
  NVL2(expr, expr1, expr2)
  expr의 값이 NULL이 아닐 경우에는 expr1의 값을 반환 하고, NULL일 경우에는 expr2의 값을 반환 한다.

- DECODE({column | expression}, search1, result1 [,search2,result2] <br>
  특정 컬럼의 값을 기준으로 마치 IF문을 사용하는 것과 같은 효과를 내는 함수


