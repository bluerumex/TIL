### JSP 4. Action Tag


```
HTML에는 없는 기능으로 자바 문법을 대신하는 JSP가 제공하는 태그들
JSP 액션 태그는 XML 스타일의 태그로 기술하며 특정한 동작 기능을 수행한다.
JSP 액션 태그는 < 와 접두어 jsp: 그리고 forward, include, param과 같은 고유한 태그 키워드로
구성되어 있다 마지막 종료는 /> 로 태그를 닫는다.

<jsp:태그키워드 태그속성="태그값" />
<jsp:include page="sub.jsp" />

액션 태그에서 매개 변수 지정과 같은 내용이 있을 경우
<jsp:include page="include.jsp">
	<jsp:param name="weeks" value="52" />
</jsp:include>

액션태그의 종류
<jsp:useBean>
<jsp:include>
<jsp:forward>
<jsp:param>


1. <jsp:include page="filename" />
현재 JSP 페이지에서 속성 page에 기술된 다른 JSP페이지를 호출하여 그 결과를 
include 태그의 위치에 삽입시키는 역할을 수행한다.

지시자 include와 액션태그 include의 차이점
<% include file="includesub.jsp" %>
지시자 include는 소스 코드 형태로 삽입하며, 액션태그는 처리결과를 삽입한다.
소스 코드 형태로 삽입되므로 중복된 소스가 있는 경우 주의가 필요하다.
변수의 선언이 중복된다거나...

액션태그 <jsp:include.../>는 내장 객체 pageContext의 메소드 include()와 같은 기능을 수행한다.
<% pageContext.include("includesub.jsp"); %>
<jsp:include page="includesub.jsp" />


2. <jsp:forward page="filename" />
태그 forwardㅇ서 지정한 페이지를 호출하면 forward 태그가 있는 현재 페이지의 작업은 모두 중지
되고, 이전에 출력한 버퍼링 내용도 모두 사라지게 되어 출력이 되지 않으며,
모든 제어가 page에 지정한 파일로 이동한다.

/forwardmain.jsp
<h2>main</h2>
<jsp:forward page="forwardsub.jsp" />

forwardsub.jsp
<h2>sub</h2>

forwardmain.jsp 페이지 오픈시 
forwardsub.jsp의 결과만 출력해서 반환.
도메인이 변하는 건 아님.


3. <jsp:param name="" value="" />
<jsp:include> 혹은 <jsp:forward>의 하위노드로 사용되며
포함하는 문서나 혹은 이동하는 문서에게 전달할 값이 있을 때 사용한다.

<jsp:include page="includesub.jsp">
	<jsp:param name="userId" value="guest" />
    <jsp:param name="passwd" value="anonymous" />
</jsp:include>

받는 페이지에서 request.getParameter("name");
```