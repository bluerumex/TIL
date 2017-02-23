### JavaScript 00. 언어의 기초

#### Boolean 연산자
```{.javascript}
boolean 연산자에는 NOT, AND, OR 세가지가 있다

1) 논리 NOT
논리 NOT 연산자는 느낌표(!)로 표시하며 ECMAScript의 모든 값에 적용가능
논리 NOT 연산자는 데이터 타입에 관계 없이 항상 boolean 값을 반환
먼저 피연산자를 boolean 값으로 변환한 다음 그 결과를 부정하며 다음과 같이 동작함.

* 피연산자가 객체이면 false를 반환
* 피연산자가 빈 문자열이면 true
* 피연산자가 비어 있지 않은 문자열이면 false
* 피연산자가 숫자 0 이면 true
* 피연산자가 0이 아닌 숫자(infinity 포함)라면 false
* 피연산자가 null 이면 true
* 피연산가 NaN 이면 true
* 피연산자가 undefined 이면 true 

ex) alert(!false)	// true
	alert(!"blue")	// false
    alert(!0)		// true
    alert(!NaN)		// true
    alert(!"")		// true
    alert(!12345)	// false
    
    
2) 논리 AND
논리 AND 연산자는 앰퍼샌드 2개(&&)로 나타낸다 다음과 같이 값 두개에 적용한다

var result = true && false;

논리 AND는 다음 표에 해당하는 값을 반환한다.
피연산자 1		피연산자 2		결과
true			true			true
true			false			false
false			true			false
false			false			false
```







