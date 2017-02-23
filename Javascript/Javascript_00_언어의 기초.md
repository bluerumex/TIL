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

논리 AND는 피연산자가 boolean이 아니어도 사용이 가능
다만 피연산자가 boolean이 아닐 때는 다음과 같이 동작하며 논리 AND가 boolean을 반환하지 않을 수도 있다.

* 첫 번째 피연산자가 객체라면 항상 두 번째 피 연산자를 반환
* 두 번째 피연산자가 객체라면 첫 번째 피연산자를 true로 평가할 수 있을 때만 
  두 번째 피 연산자를 반환
* 두 피연산자 모두 객체라면 두 번째 피연산자를 반환
* 피연산자 둘 중 하나라도 null이면 null을 반환(NaN, undefined도 마찬가지)

첫 번째 피 연산자에서 결과를 결정할 수 있다면 논리 AND 연산자는 두 번째 피연산자를 결코 평가 하지 않는다.
첫 번째 피 연산자가 false라면 두 번째 피연산자의 값과는 무관하게 절대 true일 수 없다.

var found = true; // var found = false;
var result = (found && someUndeclaredVariable) // 여기서 에러 발생
alert(result); // 이 행은 실행되지 않음

>> found가 true이므로 some...변수를 평가하려 하는데 이 단계에서 변수가 선언되지 않아 오류가 발생
>> found가 false라면 2번째 행에서 오류가 발생하지 않음 false 이므로 두번째 some..은 평가하지 않음


3) 논리 OR

논리 AND와 마찬가지로 피연산자 중 하나가 불리언이 아니라면 논리 OR에서 불리언 값을 반환하지 않을 수도 있다.

* 첫 번째 피연산자가 객체라면 첫 번째 피 연산자를 반환
* 첫 번째 피연산자가 false로 평가되면 두 번째 피연산자를 반환
* 두 피연산자가 모두 객체라면 첫 번째 피연산자를 반환
* 두 피연산자가 모두 null 이라면 null 반환(NaN, Undefined도 마찬가지)

논리 AND 연산자와 마찬가지로 논리 OR 연산자도 단축 연산을 수행한다.
첫번째 피연산자가 true로 평가된다면 두 번째 피연산자는 결코 평가하지 않는다.

피연산자 1		피연산자 2		결과
true			true			true
true			false			true
false			true			true
false			false			false

논리 OR 연산자의 특성을 이용해 변수에 null이나 undefined가 저장되지 않게 할 수 있다.
ex)
var myObject = preferredObject || backupObject;

prefferedObject가 null이 아니라면 myObject에는 prefered...값이 할당될 것이고,
null이라면 backupObject가 할당 될것이다.
```







