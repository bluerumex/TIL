### JSP 5. JSTL

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