### JSP 5. JSTL

######JSTL 개요
```
자바에서 커스텀 태그 기능을 이용하여 활용 빈도가 높은 태그를 개발한 것
자바 표준 태그 라이브러리(Java Standard Tag Library)이다.
즉 JSTL은 표준커스텀 태그라 할 수 있다.

분류
1. Core(c)  > 변수지원, 제어흐름, URL관리, 출력,예외 처리
2. XML(x) > 코아, 흐름제어, 변환
3. Internationalization(fmt) > 지역화(Locale), 메시지 포맷, 수와 날짜 포맷
4. Database(sql) > SQL
5. Functions(fn) > 집합체 길이, 문자열 처리

괄호안은 통상적으로 사용하는 접두어(prefix)

JSTL을 사용을 위한 환경설정
JSTL은 JSP 2.0의 표준 규약으로 제정되었으나, 톰캣 서버는 아직 JSTL의 표준 라이브러리를
제공하지 않으므로, JSTL 표준라이브러리를 다운 받아 톰캣 서버에 설치해야된다.(현재 톰캣은...??)

jstl.jar > JSTL API classes (JSTL API 클래스)
standard.jar > JSTL implementation classes (Standard Taglib JSTL 구현 클래스)

두개의 jar 파일을 [WEB-INF]/[lib]에 복사해서 넣는다.
```
######JSTL 태그의 사용
```
JSTL을 사용하기 위해서는 taglib 지시자를 사용해 선언해야한다.
prefix, uri는 필수, 유형은 string

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
간단한 출력 ex) <c:out value="Hello JSTL" />
```
######Core 기본 기능 태그
```
1. 변수지원
remove		-> 이미 설정한 변수를 삭제
set	   	-> 범위에서 사용될 변수를 지정

2. 제어흐름
choose		-> 태그 <when>과 <otherwise>로 구성되어 있는 여러개의 조건 중에 하나만 선정하여 처리
  when  	  -> <choose> 태그의 서브태그로 조건이 true이면 몸체를 실행
  otherwise   -> <choose> 태그의 서브태그로 이전에 있는 태그 when 조건이 모두 false일 경우
forEach	   -> 다양한 콜렉션 유형에서 반복을 처리
forTokens	 -> 문자열을 구분자로 구분하여 토큰으로 나누며 반복 실행
if			-> 조건이 true이면 몸체 실행

3. URL 관리
import		-> 다른 페이지를 현재 위치, 또는 변수 또는 읽기 객체에 저장
  param       -> 태그 <import>, <redirect>, <utl> 서브태그로, 매개변수 전송 처리
redirect	  -> 새로운 URL로 이동 처리
url		   -> 질의 매개변수를 이용하여 URL 생성

4. 예외처리, 출력
catch		 -> 예외처리
out		   -> 출력처리
```

###### 변수지원 set, remove
```language
set태그는 지정된 범위로 평가 값을 변수에 저장.
<c:set var="변수이름" value="저장할 값" scope="4개중 하나.." />

var	- 값이 저장되는 변수이름
target - 값이 저장되는 자바빈즈 객체이거나 또는 Map객체, 빈즈일경우 setter인 property에 의해 값 지정
value  - 변수 또는 객체에 저장할 값(논리 값도 저장가능 "true", "false")
property  - target 객체의 property 이름
scope  - 변수가 효력을 발휘하는 영역 page, reqeust, session, application

(상기 속성 모두 필수요소 아님)

	target의 사용 예시.
    <c:set var="book" value="<%= new java.util.HashMap() %>" />
    <c:set target="${book}" property="java" value="java로 배우는 프로그래밍 기초" />
    <c:set target="${book}" property="c" value="c......" />
    <c:set target="${book}" property="jsp" value="jsp" />
    
    ${book.java}

remove태그는 선언된 변수를 삭제하는 태그
var - 삭제할 변수이름
scope(필수 x) - 삭제할 변수의 영역 4가지 page, request, session, application
scope를 지정하면 선언시 사용했던 scope영역이랑 똑같이 지정해야 삭제됨.
```