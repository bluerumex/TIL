### jQuery 5. Event

#### 이벤트란?
```{.javascript}
이벤트는 사용자와 웹사이트 또는 웹 어플리케이션 간에 소통을 위한 주된 방법이다.
자바스크립트/jQuery 코드의 대부분은 다양한 사용자와 브라우저 이벤트를 처리하기 위해 실행될 것이다.

사용자 이벤트 - click, mousedown, keypress 등과 같은 키보드 및 마우스 상호작용을 의미,
브라우저 이벤트 - document.ready, window.onload 그리고 DOM 요소와 관련된 수 많은 다른 이벤트를 의미
```
#### 이벤트 처리기 연결하기
```{.javascript}
동일 요소에 하나 이상의 이벤트를 바인딩

jQuery('div').click(function (e)) {
	alert('event');
})
.keydown(function (e)){
	alert('event');
}

상기 코드를 간략화..
------->
function handler(e) {
	alert('event');
}

jQuery('div').click(handler).keydown(handler);
함수를 한번 정의한 뒤 여러번 참조하는 방법..

on 메서드로 간략화..
------->
jQuery('div').on('click, keydown', function(e) {
	alert('event');
});


하나 이상의 자바스크립트 이벤트와 그 이벤트가 수행하는 처리기 함수를 개체로 구성하여 
매개변수로 지정할 수도 있다.
------->
$('#two').on({
    click: function() {
        alert('click');
    },
    keydown: function() {
        alert('keydown');
    },
    keyup: function() {
        alert('keyup');
    }
})
```
#### jQuery는 이벤트를 어떻게 처리하는가?
참고자료 : Naver D2 
```{.javascript}


*jQuery의 다양한 이벤트 처리방법
일반적으로 이벤트 하나에 이벤트 핸들러 하나를 등록해 이벤트를 처리한다.
그러나 jQuery에서는 같은 이벤트를 여러번 처리하거나 같은 이벤트 핸들러를 여러 이벤트에 등록해
이벤트를 처리할 수 있다.

*네임스페이스 사용
같은 이벤트를 여러번 처리해야 할 때 jQuery에서는 이벤트를 네임스페이스로 구분할 수 있다.
'이벤트이름 + 마침표 + 네임스페이스' 형식으로 이벤트 이름 뒤에 네임스페이스를 덧 붙인다.

ex)
$(element).on('click.myPlugin', funciton() { ... });
$(element).on('click.myPlugin.myPlugin2', funciton() { ... }); 

$(element).off('click.myPlugin'); //상기 두개의 이벤트가 모두다 해제된다.
```