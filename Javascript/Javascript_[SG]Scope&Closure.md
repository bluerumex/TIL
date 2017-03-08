### JavaScript Scope, Closure

#### Scope	
```{.javascript}
다른 언어와 달리 일반적인 블록 스코프를 따르지 않음

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
```{.javascript}
function outer() {
    var count = 0;
    var inner = function() {
        return ++count;
    };
    return inner;
}

var increase = outer();
increase();	//count 1
increase();	//count 2
    
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
```