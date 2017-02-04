### JSP 1. Expression Language_02

##### 표현언어의 연산자
```
자바 언어에서 지원하는 연살자인 산술, 관계, 논리, 조건, 괄호 연산자등을 지원한다.
산술(div, mod), 논리(and, or, not)
관계 lt(less than), le(less than or equal), eq(equal), ne(not equal)
     ge(greater than or equal), gt(greater than)도 지원한다.

연산자 우선순위
1. [] .	(첨자 연산자)
2. ()
3. - ! not empty
4. * / div % mod
5. + - 
6. < <= >= > lt le e ge gt
7. == != eq ne
8. && and
9. || or
10. ? :

Empty 연산자
empty 연산자는 empty 다음의 피연산자인 표현식이 NULL 인지 검사하여 true, false를 리턴하는 연산자
정의되지 않은 표현식 n 또는 상수 NULL을 표현언어로 출력하면 아무것도 출력되지 않음

${n}
${empty n}	//true

즉 다음과 같은 표현언어에서 exp가 null 또는 null을 의미하는 값이면 true이고 아니면 false
${emtpy exp}
1. null
2. 정의되지 않은 객체
3. 빈 문자열
4. 길이가 0인 배열
5. 비어있는 집합체
```

##### 표현언어 내장 객체
| 분류 | 내장객체 | 자료유형 | 기능 |
|:--------------:|:--------------:|:--------------:|:--------------:|
| JSP page객체 | pageContext | javax.servlet.jsp.PageContext|JSP페이지 기본 객체로써, ServeltContext, session, requst, response등의 여러 객체를 참조 가능
| 범위 | pageScope , requestScope, sessionScope, applicationScope|  java.util.Map | page(requestScope, sessionScope, applicationScope) 기본 객체에 저장된 속성의 <속성, 값> 을 저장한 Map 객체, ${pageScope.속성}으로 값을 참조 |
| 요청 매개 변수| param | java.util.Map | 요청 매개변수 <매개변수이름, 값>을 저장한 Map 객체, ${param.name}은 request.getParameter(name)을 대체|
|	| paramsValues | java.util.Map | 요청 매개변수 배열을 <매개변수, 값>을 저장한 Map 객체, request.getParameterValues() 처리와 동일 |
| 요청 헤더 | header | java.util.Map | 요청 정보의 <헤더이름, 값>을 저장한 Map 객체, ${header["name"]}은 request.getHeader(헤더이름)와 같음
|	| headerValues | java.util.Map | 요청 정보 배열을 <헤더이름, 값>을 저장한 Map 객체, request.getHeaders() 처리와 동일 |
| 초기화 매개변수 | initParam | java.util.Map | 초기화 매개변수 <이름, 값>을 저장한 Map 객체, ${initParam.name}은 application.getInitParameter(name)을 대체 |
| 쿠키 | cookie | java.util.Map | 쿠키 정보의 배열을 <쿠키이름, 값>을 저장한 Map 객체, request.getCookies()의 Cookie 배열의 이름과 값으로 Map을 생성 | 

```
표현언어에서 a.b는 일반적으로 a["b"]와 가타. 표현식 a[b]의 평가는 다음의 절차를 따른다.
1. 만일 a가 Map이면 a.get(b)이다, 그러나 !a.containsKey(b)이면 null을 반환한다.
2. 만일 a가 List나 배열이면 b를 정수의 첨자로 변환하여 a.get(b)를 평가하거나 적질히
   Array.get(a, b)를 평가한다. 이 과정에서 첨자의 IndexOutOfBoundsException이 발생하면
   NULL을 반환하며, 다른 예외가 발생하면 오류가 발생한다.
3. 만일 a가 자바빈즈 객체이면 b를 문자열로 변환하여, 속성 b에 해당하는 getter인 객체의 메소드
   getB() 호출 결과를 반환하며, 이 과정에서 예외가 발생하면 오류가 발생한다.
   
표현식 a.b에서 만일 a가 표현언어의 내장 객체라면 pagecontext를 제외한 모든 내장 객체는 Map이르므로, 
모두 1의 평가과정을 거쳐 결과를 반환한다.
```