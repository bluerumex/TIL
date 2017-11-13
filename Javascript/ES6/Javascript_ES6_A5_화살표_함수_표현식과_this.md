### ECMA Script 6

>ECMAScript 6 문법

##### A.5 화살표 함수 표현식과 this
```javascript
// ES6에서는 화살표 함수 표현식(arrow function expression)을 제공하는데,
// 이 표현식을 사용하면 "익명 함수"를 좀 더 짧게 정의할 수 있고, this가 가르키는 객체를 확실하게 파악할 수 있다.
// C#이나 Java에서는 '람다 표현식'이라고 한다.

// 화살표 함수 표현식은 잔달 인자 선언과 화살표(=>), 함수 몸체로 구성된다.
// 함수의 몸체가 표현식 하나라면 중괄호를 생략할 수 있으며, 값을 반환하는 return도 생략 가능하다.

let sum = (arg1, arg2) => arg1 + arg2;

// 함수 몸체가 여러 줄이라면 중괄호가 꼭 필요하며 return 키워드도 생략할 수 없다.
(arg1, arg2) => {
	// do something
    return someResult;
}

// 전달 인자가 없다면 빈 괄호를 사용한다.
() => {
	// do something
    return someResult;
}

// 전달인자가 하나라면 괄호를 생략할 수 있다.
arg1 => {
	// do something
    return someResult;
}

var myArray = [1,2,3,4,5];
myArray.reduce((a,b) => a+b); // 15

// 매초마다 StockQuoteGenerator()의 생성자에 전달된 회사의 주식코드와 함께 임의의 주가를 출력하는
// getQuote() 함수를 실행한다.

function StockQuoteGenerator(symbol) {
    this.symbol = symbol;

    setInterval(function getQuote() {
        console.log('The price quote for ' + this.symbol + ' is ' + Math.random());
    }, 1000)
}

var stockQuoteGenerator = new StockQuoteGenerator('IBM');

// getQuote() 함수가 사용하는 this.symbol은 StockQuoteGenerator() 함수에 있는 this.symbol과 같은 변수를
// 가르키는 것 같지만, 실제로는 다른 객체를 가르킨다.
// 정확히 애기하면, getQuete() 함수가 선언되는 위치는 StockQueteGenerator() 함수 안이 아니라 
// 전역이기 때문에 getQuete() 함수에 사용된 this는 전역 객체를 가르키며, 전역 객체에 symbol 프로퍼티를 선언한 적이
// 없으므로 undefined가 출력되는 것이다.
// 해결책은 StockQueteGenerator() 함수 안에서 this를 that으로 할당해두고,
// getQuote() 함수 안에서 that.symbol로 참조하면 된다.

// 다음 코드는 상기와 같은 내용이지만, setInteval() 함수에 전달하는 콜백 함수를 선언할 때 function
// 키워드 대신 화살표 함수 표현식을 사용해서 this 문제를 해결한다

function StockQuoteGenerator(symbol) {
    this.symbol = symbol;

    setInterval(() => {
        console.log('The price quote for ' + this.symbol + ' is' + Math.random());
    }, 1000);
}

var stockQuoteGenerator = new StockQuoteGenerator('IBM');

// 화살표 함수 표현식을 사용하면 함수가 실행되는 컨텍스트를 this로 연결하기 때문에, this의 값이
// 틀어지는 상황을 방지할 수 있다.
// 위 코드에서 setInteval()에 전달된 함수에서 사용하는 this.symbol 값은 StockGenerator() 함수안에
// 선언한 것과 같이 IBM이다.
```


