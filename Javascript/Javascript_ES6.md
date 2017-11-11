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

```



