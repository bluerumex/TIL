### JavaScript Design Pattern

#### 모듈패턴
```{.javascript}
JQuery는 $자체를 하나의 변수명으로 사용하고 $변수 안에 다양한 함수를 포함하고 있다.
여러 함수와 변수를 글로벌 영역에 두고 사용하는 것이 아니라,
하나의 대표 글로벌 변수 안에 여러 함수를 두는 것이 모듈 패턴의 기본

모듈 패턴은 파일 단위로 관리할 수 있도록 자바스크립트를 모듈화 해주고,
단위 테스트를 모듈 단위로 실행할 수 있도록 해 시험 계획에 도움이 된다.
글로버 변수나 함수를 최소화 하므로 다른 스크립트 라이브러리나 소스를 가져도 쓸 때 충돌이 일어날
확률을 최소화 해준다.

* 모듈의 기본 패턴
(function (window) {
    var myLibrary = {
        helloWorld: function () {
            console.log("Hello world!");
        },
        hello: {
            world: function() {
                console.log("Hello Module!");
            }
        }
    };

    window.myLibrary = myLibrary;
}(window));

글로벌에 조금 다르게 노출
var myLibrary = (function (window) {
	var myLibrary = {
        // TODO
    };
    return myLibrary;
}(window));

var myLibrary = (function(window) {
	return {
    	// TODO
    };
}(window));
```
#### 이벤트 델리케이션 패턴
```{.javascript}
패턴의 작동원리는 이벤트 버블링을 통해 이벤트를 상위 DOM으로 전달할 수 있다는 방법에서 기인.

이벤트가 발생했을때 부모와 자식 DOM 사이에 해당 이벤트를 전파할때는
캡처링(capturing) -> 대상(target) -> 버블링(bubbling)이라는 3단계를 거침.

이벤트 버블링 : 하위 DOM -> 상위의 부모 DOM으로 한 단계씩 전파된다.
이벤트 캡처링 : 최상위 부모 DOM -> 가장 하위 DOM까지 부모에서 부터 전파된다.

이벤트 객체들은 이벤트 대상(event target)에 전달되는데, 전달되기 전에 먼저 이벤트 객체의 전파
경로가 정의된다.
전파 경로는 현재 이벤트가 전파되는 이벤트 대상들의 정렬된 목록으로, 현재 문서의 트리구조를 따라
구조적인 경로로 나타내게 된다. 전파 경로의 마지막은 이벤트 대상이며, 목록의 앞선 대상들은 현재
대상의 부모 요소들로 이루어져 있다.

특정 DOM에서 이벤트가 발생하면 해당 DOM의 dispachEvent()라는 함수를 통해서 이벤트를 전달한다.
이벤트 전달은 propaation path라는 전파 경로를 따라서 수행된다.
이벤트가 전달되는 단계는 크게 세 단계로 이루어지는데 
이벤트 캡처링이 일어나고, 그다음 이벤트 대상에 해당하는 이벤트 핸들러가 호출된 다음, 이벤트 버블링으로 이어진다.

```
