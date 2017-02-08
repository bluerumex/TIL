### jQuery 1. Selector

```{.jquery}
1. 기본적인 원리는 CSS 셀렉터를 사용

$('#content p a');
//#content안에 있는 모든 단락(p 태그) 요소 내의 모든 앵커(a 태그) 요소를 선택

TIP
$('body div#wrapper div#content');
$('#content'); 

selector를 자세하게 작성하는 것이 반드시 빠른 것이 아니다.
selector가 복잡하면 복잡할수록 jquery가 문자열을 처리하는데 더 많은 시간이 걸린다.

2.1 직속 자식 요소 찾기

직속 자손 결합자(>)
$('#nav li > a')

자손은 자식 요소내에 존재하는 또 다른 요소들을 의미.
자식은 직속 자손을 의미한다.

컨텍스트가 이미 지정되어 있다면 좌측 표현식 없이도 > 결합자를 사용할 수 있다.
$(' > p', '#content');	//$('#content > p')와 동일
$('#content').children(); //#content 요소의 모든 직속 자식을 가져온다.

TIP
children() 메서드에 셀렉터 표현식을 지정할 수 있다.
$('#content').children('p');  //#content 직계 자식들 중 단락(p) 요소만 반환


2.2 특정 형제들 선택

<h1>첫번째</h1>
<h2>두번째</h2>
<p>단락요소</p>
<h2>세번째</h2>

인접 형제 결합자(+)
$('h1 + h2');  //H1 요소에 인접한 형제 요소인 H2를 찾는다. 
(인접한 두번째 요소까지만 반환, 세번째는 반환 X)

요소의 모든 형제를 반환하는 방법
$('h1').siblings('h2, p');
$('li.selected ~ li')  //li요소 중 seleted클래스가 붙은 요소부터 뒤 따르는 모든 형제 요소 선택

TIP
next() 메서드
$('h1').next('h2');


2.3 인덱스 순서로 요소 선택하기

:first	// 첫 번째 선택 요소와 일치
:last 	// 마지막 선택 요소와 일치
:even	// 짝수 요소와 일치 (0부터 인덱스)
:odd	// 홀수

:eq(n)	//(n) 번째 인덱스에 해당하는 단일 요소와 일치
:lt(n)	// n번째 보다 밑에 있는 모든 요소와 일치
:gt(n)	// n번째 보다 위에 있는.. (n값에 음수 값도 사용 가능 1.4ver 이후)


2.4 무엇을 포함하고 있는지에 따라 요소 선택

<span>Hello Bob!</span>
$('span:contains("Bob")');	// 텍스트 콘텐츠를 검색 대소문자 구분 bob이면 검색 결과는 x
$('div:has(p a)');	// 중첩된 요소를 검사. <p>요소 안에 <a>요소를 가지고 있는 모든 <div>요소를 찾음

2.5 일치되지 않는 요소 선택
$('div:not(#content)')	//모든 #content를 제외한 div 요소 선택

:not 필터와 유사한 기능을 갖는 메서드 not()
var $anchors = $('a');
$anchors.click(function() {
	$anchors.not(this).addClass('not-clicked');
})
// 클릭된 앵커를 제외한 모든 앵커에 not-clicked 클래스를 추가

$('#nav a').not('a.active');  //not()도 마찬갖로 인자로 셀럭터를 가질 수 있다.

```