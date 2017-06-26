### JavaScript 실행컨텍스트

>실행컨텍스트는 콜 스택에 들어가는 실행 정보 하나와 비슷하다.
>ECMAScript에서는 실행 컨텍스트를 "실행 가능한 코드를 형상화하고 구분하는 추상적인 개념"으로 기술 
>콜 스택과 연관하여 정의하면, "실행 가능한 자바스크립트 코드 블록이 실행되는 환경"이라고 할 수 있고
>이 컨텍스트 안에 실행에 필요한 여러가지 정보를 담고 있다.
>여기서 말하는 실행 가능한 코드블록은 대부분의 경우 `함수`가 된다.

##### ECMAScript에서는 실행 컨텍스트가 형성되는 경우를 세가지로 규정하고 있다
 - 전역코드
 - eval() 함수로 실행되는 코드
 - 함수 안의 코드로 실행할 경우 (대부분의 경우)

현재 실행되는 컨텍스트에서 이 컨텍스트와 관련 없는 실행 코드가 실행되면, 
새로운 컨텍스트가 생성되어
스택에 들어가고 제어권이 그 컨텍스트로 이동한다.

```{.javascript}
console.log('This is global context');

function ExContext1() {
	console.log('This is Excontext1');
}

function ExContext2() {
	Excontext1();
	console.log('This is Excontext2');
}

ExContext2()
```
