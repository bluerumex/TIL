### JavaScript TIP. 01

#### Powerful JavaScript Idiomatic Expressions With && and ||
```{.javascript}
if (a > 0 || b < 0) {
// code...
}

위와 같은 경우, 앞의 연산자인 a > 0 이 참이라면, 뒤쪽 b < 0의 연산을 체크 하지 않고 { }의 
코드로 진입된다. 뒤의 b 연산을 거치지 않기 때문에 보다 효율적인 연산자라고 할 수 있다..

if (a > 0 && b < 0) {
// code...
}

마찬가지로 a > 0 false일 경우 뒤의 b연산 결과에 상관없이 { }안의 코드는 처리되지 않음..


Example 1:  || 연산을 이용한 팁

function documentTitle(theTitle) {
    if (!theTitle) {
    	theTitle  = "Untitled Document";
	}
}

parameter로 넘어온 title 값을 체크(undefined 포함) !title일 경우 그 값을 title 전역 변수에
할당하고 그렇지 않으면 else를 코드 실행

상기 코드를 단순화

function documentTitle(theTitle)
	theTitle  = theTitle || "Untitled Document";
}

앞의 논리 연산을 먼저 실행 parameter가 유효하면 전역변수 title에 해당 값을 할당한다.


Example 2: && 연산을 이용한 팁

function isAdult(age) {
	if (age && age > 17) {
    	return true;
    } esle {
    	return false;
    }
}

```



