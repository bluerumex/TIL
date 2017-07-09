### JavaScript 객체지향 프로그래밍

>자바스크립트는 프로토타입을 이용해 클래스, 생상자, 메소드, 상속 캡슐화를 구현 할 수 있다.

##### 클래스, 생성자 메서드
```javascript
// C++, Java와 같은 경우 class 키워드를 사용해 클래스를 만들 수 있다.
// 클래스와 같은 이름의 메서드로 생성자를 구현해낸다.
// 자바스크립트에는 이런 개념이없다. 자바스크립트는 거의 모든 것이 객체이고,
// 함수로 클래스, 생성자, 메소드를 구현할 수 있다.

// ---------------------------------------- 클래스 예제 ---------------------------------------- //
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

// Prototype 활용

function Person(arg) {
	this.name = arg;
}

Person.prototype.getName = function() {
	return this.name;
}

Person.prototype.setName = function() {
	this.name = value;
}

// Person prototype 프로퍼티에 getName()과 setName() 함수를 정의
// 이 Person으로 객체를 생성한다면 각 객체는 각자 따로 함수 객체를 생성할 필요없이 getName(),
// setName() 함수를 프로토타입 체인으로 접근할 수 있다

// 더글라스 크락포드는 다음과 같은 함수를 제시하면서 메서드를 정의하는 방법을 소개했다
// * 생성자로 사용되는 함수는 첫 글자를 '대문자'로 표기할 것을 권고
Function.prototype.method = function(name, func) {
	if(!this.prototype[name]) {
    	this.prototype[name] = func;
    }
}

// 이 함수를 이용한 형태
Function.prototype.method = function(name, func) {
	this.prototype[name] = func;
}

function Person(arg) {
	this.name = arg;
}

Person.method('setName', function(value) {
	this.name = value;
});

Person.method('getName', function() {
	return this.name;
});

```
##### 상속
>자바스크립트는 클래스 기반으로 하는 전통적인 상속을 지원하지는 않는다.
>하지만 자바스크립트 특성중 객체 프로토타입 체인을 이용해 상속을 구현해 낼 수 있다

```javascript
// ------------------------------ 프로토타입을 이용한 상속 -------------------------------- //

// 더글라스 크락포드의 자바스크립트 객체를 상속하는 코드
function create_object(0) {
	function F() {}
    F.prototype = 0;
    return new F();
}

// *create_object() 함수는 ECMAScript5에서 Object.create() 함수로 제공된다
// 따로 구현할 필요 없다

var person = {
	name: 'yoon',
    getName: function() {
    	return this.name;
    },
    setName: function(arg) {
    	this.name = arg;
    }
};

// function create_object(o)// *create_object() 함수는 ECMAScript5에서 Object.create() 함수로 제공된다


var person = {
	name: 'yoon',
    getName: function() {
    	return this.name;
    },
    setName: function(arg) {
    	this.name = arg;
    }
};

function create_object(o) {
	function F() {}
    F.prototype = o;
    return new F();
}

var student = create_object(person);

// 부모 객체의 메서드를 그대로 상속받아 사용하는 방법을 살펴보았다.
// 여기에 자식은 자신의 메서드를 재정의 혹은 추가로 기능을 더 확장 시킬 수 있어야 한다

student.setAge() = function(age) {...}
student.getAge() = function() {...}

// 상기 코드로 기능을 더 확장시킬 수는 있으나 이렇게 구현하면 코드가 지저분해진다
// 자바스크립트에서는 범용적으로 extend() 함수로 객체에 자신이 원하는 객체 혹은 함수를 추가 시킨다

```


