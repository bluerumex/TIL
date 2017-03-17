### JavaScript Function Methods

##### Function.prototype.apply()
```{.javascript}
Summary
주어진 this 값과 arguments로 함수를 호출
arguments에는 배열(또는 유사배열객체 array-like object)가 올 수 있다.

Syntax
fun.apply(thisArg, [argsArray])

Parameter
thisArg
	호출될 함수에게 지정될 this의 값. 호출된 함수 내에서 this가 전달된 thisArg인자와 다를 수 있으므로 주의
    만약 함수가 non-strict mode에서 실행 중이면, null과 undefined는 전역 객체로 대체되고 기본값은 래퍼객체로 대체된다

argsArray
	유사배열객체, 특히 함수가 호출될 때 생성된 arguments객체, 함수에 전달한 인자가 없는 경우는 null 또는 undefined, ECMAScript5 
```




