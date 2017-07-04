### JavaScript Scope, Closure

#### Scope
`다른 언어와 달리 일반적인 블록 스코프를 따르지 않음`
```{.javascript}
<script>
    for (var i = 0; i < 10; i++) {
        var total = (total || 0 )  + i;
        var last = i;
        if (total > 16) {
            break;
        }
    }
</script>

console.log(typeof total !== 'undefined');	// true
console.log(typeof last !== 'undefined');	// true
console.log(typeof i !== 'undefined');	// true
total === 21, last === 6
total, last, i 값에 접근가능함	// global..

블록 스코프를 생성하는 구문
* function
* with (ECMAScript 6 deprecate)
* catch
```

### Closure
>이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 `함수`를 클로저라고 한다

* 클로저는 function안에 function이 있을 때 생성된다.
* 클로저는 함수가 정의된 스코프 이외의 곳에서 호출될때 private 저장소처럼 활용 가능하다.
  이러한 경우가 발생하는 대표적인 경우
  - 내부의 function이 반환되어 바로 호출되거나 다른 곳으로 넘겨준 뒤 호출되는 경우
  - setTimeout(), setInterval() 등과 같이 함수가 비동기로 호출되는 경우
  - 이벤트 핸들러의 콜백 함수로 활용되는 경우
* 클로저를 이용해서 초기화할때는 각 상황에 따라 퍼포먼스를 고려하면 좋다.
* 클로저의 단점은 메모리와 퍼포먼스에 있다.
* 클로저는 함수가 메모리에서 없어질 때까지 유지된다.
* 같은 함수더라도 다른 클로저를 가지고 있을 수 있다.

```javascript
// ----------------------------------- Example 01 ----------------------------------- //
function outer() {
    var count = 0;
    var inner = function() {
        return ++count;
    };
    return inner;
}

// outer 함수에서 선언된 count를 참조하는 inner함수가 클로저가 된다
// 클로저로 참조되는 외부변수 즉, outer 함수의 count와 같은 변수를 자유 변수(Free variable)한다
// 이 지역 변수에 접근하려면, 함수가 종료되어 외부 함수의 컨텍스트가 반환되더라도 변수 객체는 반환
// 되는 내부 함수의 스코프 체인에 그대로 남아있어야만 접근할 수 있다. 이것이 바로 클로저다


var increase = outer();
increase();	//count 1
increase();	//count 2

// ----------------------------------- Example 02 ----------------------------------- //

function outerFunc(arg1, arg2) {
	var local = 8;
    function innerFunc(innerArg) {
    	console.log((arg1 + arg2) / (innerArg + local));
    }
    return innerFunc;
}

var exam1 = outerFunc(2, 4);
exam1(2);


```