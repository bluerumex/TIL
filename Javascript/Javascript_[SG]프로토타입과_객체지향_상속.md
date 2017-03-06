### JavaScript 프로토타입, 객체지향, 상속

#### this의 이해
```{.javascript}
함수를 호출하는 방법
* 일반 함수로의 호출
* 멤버함수로의 호출
* call() 함수를 이용한 호출
* apply() 함수를 이용한 호출	// 인자를 배열로 넘긴다.

1) 일반 함수로 호출
function say (something) {;
	alert(something);
}

say("Hello world");

2) 멤버 함수로 호출
var unikys = {
	say: function (something) {
    	alert(something)
    }
};

unikys.say("Hello world");

3) call(), apply() 함수
자바스크립트의 내장 함수로 function 객체에 기본으로 제공되는 함수이다.
Function.prototype.call
function call() { [native code] }

Function.prototype.apply
function apply() { [native code] }

call(), apply()를 이용한 say함수 호출 예

say.call(undefined, "Hello world");
say.apply(undefined, ["Hello world"]);
```