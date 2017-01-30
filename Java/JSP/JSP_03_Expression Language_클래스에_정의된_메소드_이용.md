### JSP 1. Expression Language_03

##### 표현언어에서 클래스에 정의된 메소드 이용
###### 1. 표현언어에서 이용할 함수 만들기
```
3개의 파일 필요
표현언어에서 일반적인 자바코드를 사용할 수 없다.
JSP 2.0에서 제공하는, 자바 클래스의 메소드를 태그로 정의하여 사용할 수 있다.
즉 클래스에 정의한 메소드를 표현언어에서 다음과 같이 호출하려면, 먼저 접두어
prefixname으로 태그를 선언해야 한다.

${ prefixname:functionname()}

표현언어에서 함수를 이용하려면 다음과 같이 3가지 작업을 수행한 뒤, JSP 프로그램에서
표현언어 함수를 호출할 수 있다.

1. 클래스 작성	   [Java Resource: rc]/[패키지] 
2. TLD 파일 작성	 [WebContent]/[WEB-INF]/[tld]
3. JSP 파일 작성     [WebContent]



//1. class
public class ELDatFormat {
    private static SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd(E) HH:mm:ss");

    public static String toFormat(Date date) {
        return df.format(date);
    }
}



//2. TLD 
태그 라이브러리 디스크립터(Tag Library Descriptor) 
태그 라이브러리의 정보를 기술하는 파일로 줄여서 TLD 위에서 작성한 클래스 ELDateFormat의 메소드
toFormat()을 표현언어로 이용하려면, 클래스 ELDateFormat의 메소드 toFormat을 태그로 이용한다는 정보를 
TLD 파일에 저장해야 한다. 일반적으로 [WEB-INF]하부 폴더 [tld]를 만들어 저장한다.

<function> 태그는 JSP파일에서 함수를 이용할 수 있도록 등록하는 태그로 내부에는 
<description>, <name>, <function-class>, <function-signature> 태그등이 필요하다.

<description>		: 태그를 저장하여 이용할 함수를 설명
<name>			   : 표현언어에서 직접 호출에 이용할 함수의 이름
<function-class>	 : 함수가 소속된 클래스 이름(패키지 > class)
<function-signature> : 함수의 반환유형, 이름, 인자유형인 시그네쳐

//ELfunction.tld
<?xml version="1.0" encoding="euc-kr" ?>

<taglib xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/j2eeweb-jsptaglibrary_2.0.xsd"
    version="2.0">

    <description>EL에서 함수실행</description>
    <tlib-version>1.0</tlib-version>
    <short-name>ELfunctions</short-name>
    <uri>/ELfunctions</uri>

    <function>
        <description>Date객체를 (yyyy-MM-dd(E) HH:mm:ss) 형태로 출력</description>
        <name>format</name>
        <function-class>
            com.expression.java.ELDateFormat
        </function-class>
        <function-signature>
            java.lang.String toFormat(java.util.Date)
        </function-signature>
    </function>

</taglib>



//3. JSP 파일 작성
표현언어에서 등록한 태그의 함수를 호출하려면, 가장 먼저 <taglib>태그를 이용하여 사용하
태그 접두어와 이용할 함수가 정의되어 있는 TLD 파일을 지정해야 한다.

<% taglib prefix="prefixname" uri="/WEB-INF/tld/tldfilename.tld" %>

${prefixname:functionName()}

${date.format(now)}로 함수를 호출한다.
format은 tld파일에서 <name>으로 정의된 이름..
${taglib의 속성 prefixㅇ서 지정한태그명.TLD파일에서 지정한 함수이름(인자1, 인자2, ..)}


<%@ taglib prefix="date" uri="/WEB-INF/tld/ELfunction.tld" %>

<%
    java.util.Date today = new java.util.Date();
    request.setAttribute("now", today);
%>

<h2>EL 함수 예제</h2>
[Refresh]하면 현재 시간 : ${date:format(now)} <p>


```