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
>자바스크립트는 클래스 기반으로 하는 전통적인 상속을 지원하지는 않는다
>하지만 자바스크립트 특성중 객체 프로토타입 체인을 이용해 상속을 구현해 낼 수 있다

```javascript
// ----------------------------------- 프로토타입을 이용한 상속 ------------------------------------- //

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

function create_object(o) {
	function F() {}
    F.prototype = o;
    return new F();
} // ->>

var student = create_object(person);

// 부모 객체의 메서드를 그대로 상속받아 사용하는 방법을 살펴보았다.
// 여기에 자식은 자신의 메서드를 재정의 혹은 추가로 기능을 더 확장 시킬 수 있어야 한다

student.setAge() = function(age) {...}
student.getAge() = function() {...}

// 상기 코드로 기능을 더 확장시킬 수는 있으나 이렇게 구현하면 코드가 지저분해진다
// 자바스크립트에서는 범용적으로 extend() 함수로 객체에 자신이 원하는 객체 혹은 함수를 추가 시킨다
// 다음은 jQuery의 extends() 함수를 살펴보고 활용하는 방법을 구상해보자

jQuery.extend = jQuery.fn.extend = function(obj, prop) {
    // jQuery.fn은 jQuery.prototype이다
    // extend 함수의 인자가 하나만 들어오는 경우에는 현재 객체(this)에 인자로 들어오는 객체의
    // 프로퍼티를 복사함을 의미하고, 두개가 들어오는 경우엔는 첫 번째 객체에 두 번째 객체의 프로퍼티를
    // 복사하겠다는 것을 뜻한다
	if (!prop) {
    	prop = obj;
        obj = this;
    }
    for (var i in prop) {
	    // 루프를 돌면서 prop의 프로퍼티를 obj로 복사한다
    	obj[i] = prop[i];
    }
    return obj;
}
// 이 코드에는 약점이 있다 obj[i] = prop[i];는 얕은 복사(shallow copy)를 한다
// 즉 문자 혹은 숫자 리터럴 등이 아닌 객체(배열, 함수 객체 포함)인 경우 해당 객체를 복사하지 않고 '참조'한다
// 두 번째 객체의 프로퍼티가 변경되면 첫 번째 객체의 프로퍼티도 같이 변경됨을 의미한다.
// 이것을 의도해서 작성한 경우가 아니라면, 작성자가 의도하지 않은 결과가 나오고 이를 디버깅하긴 쉬운 일이 아니다.
// 따라서 보통 extend 함수를 구현하는 경우 대상이 객체일때는 깊은 복사(deep copy)를 하는게 일반 적이다.


// -->
function extend(obj, prop) {
	// sgmdhallow Copy
    if (!prop) {
        prop = obj;
        obj = this;
    }
    for (var i in prop) {
        obj[i] = prop[i];
    }
    return obj;
}

var student = create_object(person);
var added = {
    setAge: function(age) {
        this.age = age;
    },
    getAge: function() {
        return this.age;
    }
};

// extend(student, added);
// student.setAge(25);

// extends(student);
// obj => this(Window 객체), Window 객체에 함수가 추가된다.


// ----------------------------------- 클래스 기반의 상속 ------------------------------------- //

// 클래스 기반의 상속이라고는 하나, 원리는 프로토타입을 이용한 상속과 거의 비슷하다.
// 함수의 프로토타입을 적절히 엮어서 상속을 구현, 다만 앞선 예제는 객체 리터럴로 생성된 객체의 상속을
// 예제로 들었지만, 여기서는 클래스의 역할을 하는 함수로 상속을 구현한다.

function Person(arg) {
	this.name = arg;
}

Person.prototype.setName = function(value) {
	this.name = value;
};

Person.prototype.getName = function() {
	return this.name;
};

function Student(arg) {

}

var you = new Person('iamYoon');
Student.prototype = you;

var me = new Student('yoon'); // Student {}
// 상기 코드의 문제점. 먼저 me 인스턴스를 생성할 때 부모 클래스인 Person의 생성자를 호출하지 않는다.
// 이 코드로 me 인스턴스를 생성할 때 'yoon'을 인자로 넘겼으나, 이를 반영하는 코드는 어디에도 없다.
// 결국 me 객체는 빈 객체이다.
// setNmae() 메서드가 호출되고 나서야 me 객체에 name 프로퍼티가 만들어진다.
// 이렇게 부모의 생성자가 호출되지 않으면, 인스턴스의 초기화가 제대로 이루어지지 않아 문제가 발생할 수 있다.

function Student(arg) {
	Person.apply(this, arguments);
}

// Student 함수 안에서 새롭게 생성된 객체를 apply 함수의 첫 번째 인자로 넘겨 person 함수를 실행 시킨다.
// 자식 클래스의 인스턴스에 대해서도 부모 클래스의 생성자를 실행시킬 수 있다.

// 현재는 자식 클래스의 객체가 부모 클래스의 객체를 프로토타입 체인으로 직접 접근한다.
// 하지만 부모 클래스의 인스턴스와 자식 클래스의 인스턴스는 서로 독립적일 필요가 있다.

// *두 클래스의 프로토타입사이에 중개자를 하나 만든다
Function.prototype.method = function(name, func) {
    this.prototype[name] = func;
}

Person.method('setName', function(value) {
   this.name = value;
});

Person.method('getName', function() {
    return this.name;
});

function Student(arg) {
}

function F() {};
F.prototype = Person.prototype;
Student.prototype = new F();
Student.prototype.constructor = Student;

Student.super = Person.prototype;

var me = new Student();
me.setName('yoon');
console.log(me.getName());

```
##### 캡슐화
>캡슐화란 기본적으로 관련된 여러 가지 정보를 하나의 틀 안에 담는 것을 의미한다.
>멤버 변수와 메서드가 서로 관련된 정보가 되고 클래스가 이것을 담는 큰 틀이라고 할 수 있다.
>여기서 중요한 것은 정보의 공개 여부로 정보 은닉의 개념이 바로 캡슐화이다.

```javascript
// ---------------------------------------- 캡슐화 예제 ------------------------------------------ //
var Person = function (arg) {
	// private member
    // this 객체의 프로퍼티로 선언하면 외부에서 new 키워드로 생성한 객체로 접근할 수 있다.
    // 하지만 var로 선언된 메버들은 외부에서 접근이 불가능하다.
    var name = arg ? arg : 'yoon';

	// public 메소드가 클로저 역할을 하면서 private 멤버인 name에 접근 할 수 있다.
    this.getName = function() {
        return name;
    }
    this.setName = function(arg) {
        name = arg;
    }
};

var me = new Person();
console.log(me.getName());
me.setName('iamyoon');
console.log(me.getName());
console.log(me.name); // undefined

// 상기 코드를 다듬은 형태
var person = function(arg) {
	var name = arg ? arg : 'yoon';

    return {
    	getName: function() {
        	return name;
        },
        setName: function(arg) {
        	name = arg;
        }
    };
}

var me = new Person(); /* or var me = new Person(); */
```

