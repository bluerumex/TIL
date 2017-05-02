### JavaScript 기본_함수와 프로토타입 체이닝

#### 함수 선언
```{.javascript}
자바스크립트의 함수는 모듈화 처리나 클로저, 객체 생성 등 자바스크립트의 근간이 되는 많은 기능을 제공하고 있다

함수를 생성하는 3가지
1) 함수 선언문 function statement
2) 함수 표현식 function expression
3) Function() 생성자 함수

*자바스크립트에서는 함수도 하나의 값처럼 취급된다.

//함수 선언문
funcion add(x, y) {
	return x + y;
}

//함수 표현식
var add = function(x, y) { // 익명 함수 표현식
	return x + y;
}

> 내부적으로 
var add = function add(x, y) {...} 자바스크립트 엔진에 의해 add 기명이 내부적으로 붙음

var plus = add;	// 함수 변수라고 한다. 함수 add는 함수의 참조값을 가지므로 또 다른 변수에 할당 가능
add(5, 2)	// 결과 - 7
plus(5, 2)	// 결과 - 7

var add = function sum(x, y) { // 기명 함수 표현식
	return x + y;
}

sum(2, 3) // Uncaught ReferenceError : sum is not defined 에러 발생
함수 표현식에서 사용된 함수 이름이 외부 코드에서 접근 불가능

함수 표현식에서 함수 이름이 선택사항이지만, 함수 이름을 이용하면 함수 코드 내부에서 함수 이름으로
함수의 재귀적인 호출이 가능하다.

var factorialVar = function factorial(n) {
	if(n <= 1) {
    	return 1;
    }
    return n * factorial(n-1);
};

//Function() 생성자 함수를 통한 함수 생성
new Function (arg1, arg2, ... argN, functionBOdy)

var add = new Function('x', 'y', 'return x + y');
```
#### 함수 객체
```{.javascript}
함수도 객체다. 
함수의 기본 기능인 코드 실행뿐만 아니라, 함수자체가 일반 객체처럼 프로퍼티들을 가질 수 있다.

function add(x, y) {
	return x + y;
}

add.result = add(3, 2);
add.status = 'OK';

함수도 객체처럼 취급 되기 때문에 다음과 같은 동작이 가능하다.
* 리터럴에 의해 생성
* 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능
* 함수의 인자로 전달
* 함수의 리턴값으로 리턴가능
* 동적으로 프로퍼티를 생성 및 할당 가능
```
#### 프로토타입 체이닝
```{.javascript}
자바스크립트는 프로토타입 기반의 객체지향 프로그래밍을 지원한다.

자바스크립트의 모든 객체는 자신의 부모인 프로토타입 객체를 가리키는 참조 링크 형태의 숨겨진 프로퍼티가 있다.

```
#### 함수 호이스팅(hoist)
```{.javascript}
모든 변수는 함수 본문 어느 부분에서 선언(declaration)이 되더라도 내부적으로 함수의 맨 윗부분으로
끌어올려(hoist)진다.
함수 선언문을 사용하면 변수 선언뿐 아니라 함수 정의 자체도 호이스팅되기 때무에 자칫 오류를 만들어 낼 수 도 있다.

// anti pattern
function foo() {
	alert('global foo');
}
function bar() {
	alert('globar bar');
}

function hoistMe() {
	console.log(typeof foo); // "function"
    console.log(typeof bar); // "undefined"
    
    foo(); // "local foo"
    bar(); // TypeError: bar is not a function
    
    // 함수 선언문
    // 변수 'foo'와 정의된 함수 모두 호이스팅된다.
    function foo() {
    	alert('local foo');
    }
    
    // 함수 표현식
    // 변수 'bar'는 호이스팅 되지만 정의된 함수는 호이스팅되지 않는다.
    var bar = function() {
    	alert('local bar');
    };
}

hoistMe();

```