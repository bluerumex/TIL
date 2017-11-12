### ECMA Script 6

>ECMAScript 6 문법

##### A.4 변수 스코프
```java
// A4.1 호이스팅
// ES5에서 변수의 스코프는 항상 애매한 문제였다.
// ES5에서는 변수를 선언한 위치와 관계없이 var 키워드가 스코프의 제일 위로 옮겨져 선언 되는데
// 이것을 호이스팅이라고 한다.
// this 키워드의 사용도 Java나 C#과 다르게 직관적이지 않았다.

// ES6에서는 let을 도입해서 호이스팅에 대한 혼란을 없애고 this에 대한 애매함도 화살표 함수
// (arrow function)을 도입해서 해결했다.

function foo() {
    for (var i = 0; i < 10; i++) {
    }

    console.log('i=' + i);
}

// 코드를 실행하면 i = 10이라는 결과가 출력된다.
// i 변수는 for 루프 안에서 사용하기 위해 만들어진 것이 확실하지만, for 루프 밖에서도
// 여전히 접근할 수 있다. ES5에서는 언제나 변수 선언을 스코프의 제일 위로 끌어올린다.

var customer = 'joe';

(function() {
    console.log('The name of the customer inside the function is ' + customer);

    if (2 > 1) {
        var customer = 'Mary';
    }

})();

console.log('The name of the customer outside the function is ' + customer);

The name of the customer inside the function is undefined
The name of the customer outside the function is joe

// 중괄호 안에 또 다른 customer 변수를 선언하면, 함수 범위안에는 전역 범위에서 가져온 변수와 지역 범위에 선언된
// 변수의 이름이 같다. 함수 안의 customer 변수 값은 undefined가 된다.

// ES5에서는 변수 선언이 선언 범위의 제일 위로 끌어 올려지지만, 변수의 초기화는 변수가 선언된 위치에서 처리된다.
// 그래서 undefined가 출력

var doSomething = function() {
    console.log("I'm doing something");
};

// 함수를 변수에 할당해서 사용하는 경우에는, 변수 선언은 호이스팅되만 함수의 몸체를 할당하는 동작은
// 변수 초기화와 마찬가지로 호이스팅되지 않는다.
// doSomething 함수를 실행하면 undefined를 실행하기 때문에 에러가 발생한다.


// A4.2 let과 cosnt를 사용하는 변수 스코프

```


