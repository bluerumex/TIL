### ECMA Script 6

>ECMAScript 6 문법

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