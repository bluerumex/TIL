### jQuery 3. Create Basic Plugin

```language
본 문서는 http://learn.jquery.com/plugins/basic-plugin-creation/
```

#####  How jQuery Works 101 : jQuery Object Methods
```{.javascript}
jQuery의 작동
$('a').css("color", "red");

$함수는 요소를 선택할 때 사용하고 jQuery 객체를 반환한다.
또한 객체는 .css(), .click()과 같은 메서드들을 포함.
jQuery 객체는 $.fn 객체로 부터 이런 메소드들을 받는다.
```
##### Basic Plugin Authoring
```{.javascript}
텍스트를 초록색으로 바꾸는 plugin을 만든다고 가정 
greenity를 $.fn로 호출하는 함수를 추가합니다. 
그러면 다른 jQuery 객체 메소드와 마찬가지로 사용이 가능해진다.

$.fn.greenity = function() {
	this.css("color", "green");
};

$('a').greenity();

.css()나 다른 메소드를 쓸 때 this를 쓰지 $(this)를 쓰지 않는다.
greenity 함수는 .css()와 같은 객체이기 때문?

차이점이 정확히 이해되지 않는다 상기 코드에 $(this)를 써도 코드는 이상없이 작동한다...
```
##### Chaining
```{.javascript}
잘 실행이 되나 더 다른 작업을 해줘야 할 필요가 있다.
jQuery이 특징인 chaining이 가능하게 작업해 보자.

모든 jQuery 객체 메소드가 원래 jQuery 객체를 다시 반환한다.
(몇가지 예외도 있음 .width()는 파라미터 없이 선택된 요소의 너비를 반환하며 chaining 되지 않음)

상기 greenify 코드를 chainable하게 만들어보자

$.fn.greenity = function() {
	this.css("color", "green");
    return this; // chaining을 위해 현재 객체를 반환
};

$('a').greenify().addClass('greenified');
```
##### Protecting the $ Alias and Adding Scope
```{.javascript}
$ 변수는 Javascript 라이브러리에서 광범위하게 사용되고 있다.
jQuery와 다른 라이브러리와 함께 사용한다면 jQuery에서 $를 사용하지 못하도록
jQuery.noConflict()를 사용해야 한다.
하지만 이럴 경우 $는 jQuery함수의 별칭이라는 가정으로 플러그인을 만들고 있으므로
코드를 망가뜨리게 된다.

다른 플러그인과 잘 작동하게 하기 위해, 그리고 jQuery를 $기호와 계속 쓰기 위해 우리는
우리 코드안에 IIFE(Immediately-Invoked Function Expression)을 넣어 $를 파라미터명으로
정하고 jQuery함수에 넘겨야 한다.

(function ($) {
	$.fn.greenity = function() {
	this.css("color", "green");
    return this; // chaining을 위해 현재 객체를 반환
};
}(jQuery));


초록색 이외의 색을 넣는다고 가정할 경우 변수에 넣어보자.

(function ($) {
	var shade = "#556b2f";
	$.fn.greenity = function() {
	this.css("color", shade);
    return this; // chaining을 위해 현재 객체를 반환
};
}(jQuery));
```
##### Minimizing plugin Footprint
```{.javascript}
$.fn에서 하나의 슬롯만(bracket을 의미?) 사용하여 플러그인을 만드는 것은 매우 좋은 습관이다.
플러그인이 오버라이드 될 확률과, 다른 플러그인을 오버라이드 할 확률을 줄여주기 때문.

다음 경우는 매우 좋지 않은 케이스

(funtion ($) {
	$.fn.openPopup = function() {
    	// open popup code.
    };
    $.fn.closePopup = function() {
    	// close popup code.
    };
}(jQuery))

다음과 같이 하나의 슬롯으로 작성
파라미터를 이용하여 하나의 슬록이 액션을 수행하도록 만드는 것이 낫다.

$(function ($) {
	$.fn.popup = function(action) {
    	if (action == "open") {
        	//open popup code
        }
        if (action == "close") {
        	//close popup code
        }
    };
}(jQuery));
```
##### Using the each() Method
```{.javascript}
jQuery 객체는 보통 DOM 요소의 수에 대한 참조를 포함하고 있다. (컬렉션)
특정 요소에 어떤 조작을 수행(테이터 속성을 받거나, 특정 위치를 계산하는 작업)을 하려고 한다면
.each()를 이용해 요소 반복해야 한다.

$.fn.newPlugin = function() {
	return this.each(function() {
  		// do something to each element here.  
    });
};

this를 반환하는 것 대신 .each()의 결과를 반환하게 된다는 것에 유의.
each()는 이미 chainable하기 때문에, 우리가 반환할 값 this를 반환한다.
```
##### Accepting Options
```{.javascript}
플러그인이 더욱 복잡해 진다면, 옵션들을 통해 커스터마이징이 가능하게 만드는 것도 좋은
아이디어이다. 이런 일을 하기 위한 가장 쉬운 방법은 객체 리터럴을 이용하자
greenify 플러그인을 몇가지 옵션을 받을 수 있게 변경.

(function ($) {
	$.fn.greenify = function(options) {
    	//This is the easiest way to have default options.
        var settings = $.extend({
        	//These are the default.
            color: "#556b2f",
            backgroundColor: "white"
        }, options);
        
        //Greenify the collection based on the settings variable.
        return this.css({
        	color: settings.color,
            backgroundColor: settings.backgroundColor
        });
    };
}(jQuery));

$('div').greenify({
	color: "orange"
});

color의 기본 값은 #556b2f이지만, $.extend()로 오버라이드 되어 orange로 변경됨.
```
