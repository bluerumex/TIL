### JavaScript 03. 함수형 프로그래밍

#### 개념
```{.javascript}
함수의 조합으로 작업을 수행함을 의미.
*작업이 이루어 지는 동안 작업에 필요한 데이터와 상태는 변하지 않는다.
변할 수 있는 건 오로지 함수뿐이다.
이 함수가 바로 연산의 대상이 됨.

자바스립트에서 함수형 프로그래밍이 가능한 이유는?
* 일급 객체로서의 함수
* 클로저

ex)

function reduce(func, arr, memo) {
    var len = arr.length;
    var i = 0;
    var accum = memo;

    for (; i < len; i++) {
        accum = func(accum, arr[i]);
    }

    return accum;
}

var arr = [1, 2, 3, 4];

var sum = function (x, y) {
    return x + y;
};

var multiply = function(x, y) {
    return x * y;
};

console.log(reduce(sum, arr, 0));
console.log(reduce(multiply, arr, 1));

```



