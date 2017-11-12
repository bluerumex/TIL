### ECMA Script 6

>ECMAScript 6 문법

##### A.2 템플릿 문자열
```javascript
// 문자열을 사용하는 새로운 문법을 제공하는데 이 기능은 문자열 삽입(string interpolation)이라고 한다
// ES5에서 문자열 안에 변수의 값을 넣으려면 문자열을 조합해야했다

var customerName = 'john smith';
console.log('Hello' + customerName);

// 역따옴표(backtick)를 사용하는 템플릿 리터럴에서는 $기호와 ({,})를 사용해 문자열 안에 표현식을 넣을 수 있다
var customerName = 'john smith';
console.log(`Hello ${customerName}`);

function getCustomer() {
	return 'allan lou';
}
console.log(`Hello ${getCustomer()}`);

// A.2.1 여러 줄에 걸친 물자열
// 문자열은 여러 줄에 걸쳐 작성 할 수 있다. 역따옴표를 사용하면 문자열을 더하는 연산이나 백슬래시를 사용하는 줄바꿈 없이도
// 문자열을 여러줄로 작성할 수 있다
// 출력된 문자열은 모든 공백을 그대로 유지한다

var message = `Please enter the password that
               has at least 8 characters and
               includes a capital letter`;
console.log(message);


// A.2.2 태그가 붙는 템플릿 스트링
템플릿 스트링 앞에 함수 이름을 붙이면, 문자열이 먼저 처리되고 이 문자열을 인자로 전달하면서 함수로 사용할 수 있다.
이때 템플릿의 문자열 요소는 각 배열의 항목으로 변환되어 전달되는데, 일반적인 함수 호출과 다르다기 때문에 어색할수 있다

mytag`Hello ${name}`;

function currencyAdjustment(stringParts, region, amount) {
    console.log(stringParts);
    console.log(region);
    console.log(amount);

    var sign;
    if (region === 1) {
        sign = '$';
    } else {
        sign = '\u20AC';
        amount = 0.9 * amount;
    }

    return `${stringParts[0]}${sign}${amount}${stringParts[2]}`;
}

var amount = 100;
var region = 2;

다음과 같이 호출이 가능하다
var message = currencyAdjustment`you've earned ${region} ${amount}`;

"you've earned €90"
```
##### A.3 옵션 인자와 인자 기본값
```javascript
// ES6에서는 함수에 인자가 전달되지 않았을때 사용할 인자의 기본값을 지정할 수 있다.
function calcTaxES5(income, state) {
    state = state || 'Florida';
    console.log('ES5. Calculating tax for the resident of ' + state + ' with the income ' + income);
}

// ES6
function calcTaxES6(income, state = 'Florida') {
    console.log('ES6. Calculating tax for the resident of ' + state + ' with the income ' + income);
}

// state 인자값에 특정값을 하드코딩하지 않고 함수를 사용할 수도 있다.
// state = getDefaultState();

function getDefaultState() {
	return 'Florida';
}

// 다만 이 경우에는 함수가 실행될때마다 인자값을 가져오는 함수도 실행되므로
// 성능에 신경써야 된다
```
##### A.4 변수 스코프
```java
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
// 
```


