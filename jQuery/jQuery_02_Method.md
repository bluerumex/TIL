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


```