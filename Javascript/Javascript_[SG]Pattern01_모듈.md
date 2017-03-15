### JavaScript 모듈패턴

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