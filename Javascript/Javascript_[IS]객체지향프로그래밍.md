### JavaScript 객체지향 프로그래밍

>자바스크립트는 프로토타입을 이용해 클래스, 생상자, 메소드, 상속 캡슐화를 구현 할 수 있다

##### 클래스, 생성자 메서드
```javascript
// C++, Java와 같은 경우 class 키워드를 사용해 클래스를 만들 수 있다.
// 클래스와 같은 이름의 메서드로 생성자를 구현해낸다.
// 자바스크립트에는 이런 개념이없다. 자바스크립트는 거의 모든 것이 객체이고,
// 함수로 클래스, 생성자, 메소드를 구현할 수 있다.

// ----------------------------------- 클래스 예제 ----------------------------------- //
function Person(arg) {
	this.name = arg;

    this.getName = function() {
    	return this.name;
    }

    this.setName = function(value) {
    	this.name = value;
    }
}

var me = new Person('yoon');
console.log(me.getName());	// yoon

me.setName('wook');

// 이 형태는 기존 객체지향 프로그래밍언어에서 한 클래스의 인스턴스를 생성하는 코드와 매우 유사하다
// 함수 'Person'이 클래승자 생성자의 역할을 한다.
// 하지만 상기 예제에는 문제가 있다.
// Person 객체를 여러개를 생성했다고 가정했을 때, 각 객체에는 자기 영역에서 공통적으로 사용할 수
// 있는 setName(), getName() 메소드를 각 객체마다 따로 생성하고 있다.
// 이는 불 필요하게 중복되는 영역을 메모리에 올려놓기 때문에 자원의 낭비가 이루어진다.


```
##### title
```javascript
```


