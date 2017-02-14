### jQuery 2. Method

```{.jquery}
1. 선택된 결과의 집합을 루프 돌면서 처리

$().each(); 메서드

$("div#post a[href]").each(function (i)) {
	urls[i] = $(this).attr('href');
}

$().each(); 메서드를 사용해 jQuery 개체에 있는 각 요소를 반복하여 처리함으로써 배열을
만들 수 있다.

*().each();는 jQuery 유틸리티 메서드인 jQuery.each(objcet, callback);과는 다르다
jQuery.each 메서드는 배열과 개체 둘다 반복하여 처리할 수 있는 일반적인 반복 메서드이다.


2. 선택집합을 특정 항목들로 줄이기

jQuery를 사용해 선택집합을 만든후 .eq() 메서드를 체인으로 연결하면서 원하는 항목의 인덱스를
매개 변수로 지정하면 된다.

jQuery 1.4에서는 인덱스 값으로 음수를 지정하는게 가능
-1은 선택집합의 마지막 요소를 의미, -2는 끝에서 두번째...


3. 선택된 jQuery 개체를 원래의 DOM 개체로 변환

jQuery로 페이지 요소를 선택하면 원래의 DOM 개체가 아닌 jQuery 개체로 된 집합을 반환한다.
jQuery 개체는 jQuery 메서드만 실행할 수 있다. 선택된 집합에 대해 DOM 메서드와 속성을
실행하기 위해서는 이를 원래의 DOM개체로 변환

$.get(index)를 사용해 단일 요소의 DOM 개체를 가져올 수 있긴하지만,
관례적으로 $('div')[1] 과 같이 [] 표기법을 사용

<ol>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
    <li>8</li>
    <li>9</li>
    <li>10</li>
</ol>

var lis = $('ol li').get().reverse(); //reverse() 자바스크립트 메서드 역순정렬
$('ol').empty();
$.each(lis, function(i) {
    $('ol').append("<li>" + lis[i].innerHTML + "</li>");
});


4. 선택집합에서 항목의 인덱스 얻기

$('div').click(function() {
	alert($('div').index(this));
})


5. 기존 배열로부터 고유한 배열 만들기

var arr = $.map($('li'), function(item, index) {
	while (index < 3) {
    	reutnr $(item).html();
    }
    return null;
.
$(document.body).append("'"<span>The first three 
						authors are : " + arr.join(', ') + "</span>");


6. 선택된 집합의 일부에 대해 동작 수행하기

$('p').slice(1, 3).wrap("<i></i>");
//인덴스가 1부터 3 이전까지 부분집합을 선택한 후 그 집합들을 이탤릭 태그로 감싼다.


7. jQuery가 다른 라이브러리와 충돌하지 않도록 설정

1) jQuery.noConflict(); 메서드

jQuery.noConflict();
jQuery(document).ready(function() {
	jQuery("div#jQuery").css("font-weight", "bold");
});

jQuery.noConflict()를 호출하는 경우 $변ㅅ를 가장 먼저 구현하고 있는 라이브러리에게 그에
대한 제어권을 양보한다.

2) 지정하고 싶은 짧은 이름을 변수로 정의

var j = jQuery.noConflict();

j(document).ready(function() {
	j("div#jQuery").css("fot-weight", "bold");
});


3) jQuery 코드를 클로저 내부로 캡슐화 하는 방법

(function($) {
	$('div#jQuery').css("font-weight", "bold");
})(jQuery);

클로저를 사용하면 함수 내부에서 실행되는 동안에만 jQuery 개체에 사용할 수 있는 $변수를
임시로 만들 수 있다. 함수가 종료되면 $변수는 애초에 제어권을 갖고 있는 라이브러리의 것으로 
인식.

* 캡슐화된 함수 안에서 $를 요구하는 다른 라이브러리의 메서드는 사용할 수 없다.
```