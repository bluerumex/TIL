### Cascading Style Sheet Media Query

>출력 장치의 여러 특징 가운데 일부를 참조해 CSS 코드를 분기 처리함으로써
하나의 HTML 소스가 여러가지 뷰를 갖도록 구현할 수 있는 명세이다.

##### CSS 코드 내부에서 분기하는 방법
```html
기본적인 문법
@media only all and (조건문) {실행문...}

only : only 키워드는 미디어쿼리를 지원하는 사용자 에이전트만 미디어 쿼리 구문을 해석하라는 명령이며 생략 가능하다. 
(생략시 기본값은 only)로 처리된다.
생략해도 무방하므로 이 키워드는 일반적으로 작성하지 않는다.
이 자리에 not 키워드를 사용할수 있는데 뒤에 오는 모든 조건을 부정하는 연산을 한다.

all (미디어 타입) : all 키워드는 미디어 쿼리를 해석해야 할 대상 미디어를 선언한 것이다.
all 이면 모든 미디어가 이 구문을 해석해야 한다. (생략가능하며 생략시 기본값은 all)로 처리된다.
쉼표(,)를 통해서 미디어 타입을 나열하면 나열한 모든 미디어 타입을 뜻함

- 미디어 타입의 종류
	- all : 모든 미디어 타입
	- aural : 음성 합성 장치
	- braille : 점자 표시 장치
	- handheld : 손으로 들고 다니면서 볼 수 있는 작은 스크린에 대응하는 용도
	- print : 인쇄 용도
	- rojection : 프로젝터
	- screen : 컴퓨터 스크린 (가장 많이 사용 대부분의 컴퓨터와 모바일 기기를 뜻함)
	- tty, tv, embrossed .. 등이 있다

조건문(속성 : 속성값) :
(min-width: 400px) 형태로 선언

- 속성과 속성값
	- width : 웹페이지의 가로 길이를 판단
	- height : 웹페이지의 세로 길이를 판단
	- device-width : 단말기의 물리적인 가로 길이를 판단. 기기의 실제 가로 길이를 판단
	- device-height
	- orientation : width와 height를 구하여 width 값이 길면 landscape로, heigth 값이 길면 portrait로 판단
	- aspect-ratio : width/height 비율을 판단
	- device-aspect-ratio : 단말기의 물리적인 화면 비율을 판단
	- color-index : 단말기에서 사용하는 최대 색상수를 판단
	- monochrom : 흑백 컬러만을 사용하는 단말기에서 흰색과 검은색 사이의 단계를 판단
	- resolution : 지원하는 해상도를 판단. 값으로 dip(인치당 도트 수) dpcm(cm당 도트 수)를 사용
	* color : 단말기에서 사용하는 최대 색상 수의 비트 수를 판단. (자연수를 쓰지만 2의 지수를 뜻함) ex) 1은 2, 2는 4, 3은 8...

미디어 쿼리 속성은 프로그래밍 언어와 같이 =, >, < 등의 연산자를 사용하지 않으며
속성 명 앞에 min- 또는 max-를 붙여서 최소값, 최대값을 판단
속성은 and (속성: 속성값) and (속성: 속성 값)으로 나열할 수 있으며 min- , max-를 이용 할 경우 범위로도 설정이 가능
resolution 같은 기능이 필요한 이유는 아이폰3와 아이폰4 같이 화면의 크기는 같지만 지원하는 해상도가 다른 기기의 경우를 판단할 때 사용하면 좋다.
```

```javascript
@charset “utf-8”;
/* All Device */
모든 해상도를 위한 공통 코드를 작성한다. 모든 해상도에서 이 코드가 실행됨.
/* Mobile Device */
768px 미만 해상도의 모바일 기기를 위한 코드를 작성한다. 모든 해상도에서 이 코드가 실행됨. 미디어 쿼리를 지원하지 않는 모바일 기기를 위해 미디어 쿼리 구문을 사용하지 않는다.
/* Tablet & Desktop Device */
@media all and (min-width:768px) {
사용자 해상도가 768px 이상일 때 이 코드가 실행됨. 테블릿과 데스크톱의 공통 코드를 작성한다.
}
/* Tablet Device */
@media all and (min-width:768px) and (max-width:1024px) {
사용자 해상도가 768px 이상이고 1024px 이하일 때 이 코드가 실행됨. 아이패드 또는 비교적 작은 해상도의 랩탑이나 데스크톱에 대응하는 코드를 작성한다.
}
/* Desktop Device */
@media all and (min-width:1025px) {
사용자 해상도가 1025px 이상일 때 이 코드가 실행됨. 1025px 이상의 랩탑 또는 데스크톱에 대응하는 코드를 작성한다.
}

```
```javascript
Andy Clarke의 기기별 미디어 쿼리
분류는 크게 데스크탑 브라우저, iPhone, iPad, 스마트폰(저해상도, 고해상도)로 구분

/* 스마트폰 가로+세로 */
@media only screen and (min-device-width : 320px) and (max-device-width : 480px){
}

/* 스마트폰 가로 */
@media only screen and (min-width : 321px) {
}

/* 스마트폰 세로 */
@media only screen and (max-width : 320px) {
}

/* iPhone4와 같은 높은 크기 세로 */
@media
only screen and (-webkit-min-device-pixel-ratio : 1.5),
only screen and (min-device-pixel-ratio : 1.5) {
}

/* iPhone4와 같은 높은 해상도 가로 */
@media only screen and (min-width : 640px) {
}

/* iPad 가로+세로 */
@media only screen and (min-device-width : 768px) and (max-device-width : 1024px) {
}

/* iPad 가로 */
@media only screen and (min-device-width : 768px) and (max-device-width : 1024px) and (orientation : landscape) {
}

/* iPad 세로 */
@media only screen and (min-device-width : 768px) and (max-device-width : 1024px) and (orientation : portrait) {
}

/* 데스크탑 브라우저 가로 */
@media only screen and (min-width : 1224px) {
}

/* 큰 모니터 */
@media only screen and (min-width : 1824px) {
}
```
_ _ _
참고 사이트
- http://naradesign.net/wp/2012/05/30/1823/
- http://www.nextree.co.kr/p8622/
_ _ _







