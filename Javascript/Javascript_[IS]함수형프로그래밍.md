### JavaScript 함수형 프로그래밍

>함수형 프로그래밍은 함수의 조합으로 작업을 수행함을 의미한다.
>중요한 것은 이 작업이 이루어지는 동안 필요한 데이터와 상태는 변하지 않는다는 점이다.
>변할 수 있는것은 오직 함수뿐이다.

##### 개념
```javascript
// 함수형 프로그래밍을 표현하는 슈도 코드
// 특정문자열을 암호화하는 함수가 여러개 있다고 가정

f1 = encrypt1;
f2 = encrypt2;
f3 = encrypt3;

// f1, f2, f3은 입력값이 정해지지 않고, 서로 다른 암호화 알고리즘만 있다.

pure_value = 'yoon'; // 암호화할 문자열
encrypted_value = get_encrypted(f1);

// pure_value는 작업에 필요한 데이터고 작업이 수행되는 동안 변하지 않는다.
// get_encrypted()가 작업하는동안 변할 수 있는 것은 오로지 입력으로 들어오는 함수뿐이다.

// f1, f2, f3는 외부(pure_value)에 아무런 여향을 미치지 않는 함수라 할 수 있다.
// 이를 순수함수(Pure function)라고 한다. 외부에 영향을 미치지 않으므로 이미 작성된 함수로
// 다른 작업에 활용해도 문제가 없다.

// get_encrypted() 함수는 인자로서 f1, f2, f3 함수를 받는다.
// 결과값이 encrypted_value라는 값이지만 결과값을 또 다른 형태의 함수로 반환할 수 있다.
// 함수를 또 하나의 값으로 간주하여 함수의 인자 혹은 반환값으로 사용할 수 있는 함수를
// 고계함수(High-order function)이라 한다.

// 개발자는 입력으로 넣을 암호화 함수를 새롭게 만드는 방식으로 암호화 방법을 개선할 수 있다.
// 내부 데이터 및 상태는 그대로 둔채 제어할 함수를 변경 및 조합함으로써 원하는 결과를 얻어내는
// 것이 함수형 프로그래밍의 중요한 특성이다.

// ----------------------------------- 1. 배열의 각 원소 총합 구하기 ----------------------------------- //

// 배열의 각 원소 총합 구하기
function sum(arr) {
    var len = arr.length;
    var i = 0, sum = 0;

    for (; i < len; i++) {
        sum += arr[i];
    }

    return sum;
}

var arr = [1,2,3,4];
console.log(sum(arr)); // 출력값 10

// 일반적인 총합 구하기 방식
// 추가로 각 원소를 모두 곱한 값을 구한다고 가정하자

function multiple(arr) {
	var len = arr.length;
    var i = 0, result = 1;

    for (; i < len; i++) {
    	result *= arr[i];
    }

    return result;
}

// 문제 하나하나를 각각의 함수를 구현하여 문제를 풀고 있다.
// 함수형 프로그래밍을 이용해 다시 코드를 작성해보자.

function reduce(func, arr, memo) {
	var len = arr.length,
    	i = 0,
        accum = memo;

    for (; i < len; i++) {
    	accum = func(accum, arr[i]);
    }

    return accum;
}

var arr = [1,2,3,4];

var sum = function(x, y) {
	return x + y;
};

var multiply = function(x, y) {
	return x * y;
};

console.log(reduce(sum, arr, 0));
console.log(reduce(multiply, arr, 1);


// --------------------------------------------- 2. 팩토리얼 --------------------------------------------- //

function fact(num) {
	var val = 1;
    for (var i = 2; i <= num; i++) {
    	val = val * 1;
    }
    return val;
}

```


