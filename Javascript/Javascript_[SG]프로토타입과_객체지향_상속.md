### JavaScript 프로토타입, 객체지향, 상속

#### this의 이해
```{.javascript}
함수를 호출하는 방법
* 일반 함수로의 호출
* 멤버함수로의 호출
* call() 함수를 이용한 호출
* apply() 함수를 이용한 호출	// 인자를 배열로 넘긴다.

1) 일반 함수로 호출
function say (something) {;
	alert(something);
}

say("Hello world");

2) 멤버 함수로 호출
var unikys = {
	say: function (something) {
    	alert(something)
    }
};

unikys.say("Hello world");

3) call(), apply() 함수
자바스크립트의 내장 함수로 function 객체에 기본으로 제공되는 함수이다.
Function.prototype.call
function call() { [native code] }

Function.prototype.apply
function apply() { [native code] }

call(), apply()를 이용한 say함수 호출 예

say.call(undefined, "Hello world");
say.apply(undefined, ["Hello world"]);

call, apply 함수의 첫번째 인자를 undefined로 넘기면 this의 기본값으로 window가 설정된다.

* this는 함수나 스코프 기반으로 결정되는 것이 아니라 호출방법에 따라 변경된다.

```
#### Prototype
```{.javascript}
다른 객체들과 공유되는 속성을 제공하는 객체이다.
생성자가 객체를 생성할 때, 객체는 내부적으로 생성자의 prototype 속성을 활용하여 속성들의 
레퍼런스를 참조한다. 생성자의 prototype 속성은 constructor.prototype과 같은 표현식으로
프로그램 내에서 접근이 가능하고, 객체의 prototype에 추가된 속성은 상속받는 객체들까지 함께 공유된다.

* Prototype Chain
객체내의 속성 탐색 순서
일단 객체 자체의 속성부터 찾은다음, 있으면 그 속성을 참조하고 없으면 자신의 프로토타입에 저장된
속성들을 검사한다. 그리고 거기에도 없으면 undefined를 반환

자바스크립트에서 모든 객체는 프로토타입이라는 다른 객체(또는 null)를 가리키는 내부 링크를 가지고 있다.
한 객체의 프로토타입 또한 프로토타입을 가지고 있고, 이것이 반복되다 null을 프로토타입으로 가지는 객체
에서 끝난다 이를 Prototype chain이라 한다.

function Car() {
    this.wheel = 4;
    this.beep = "Car_BEEP";
};

Car.prototype.go = function () {
    console.log(this.beep);
};

function Truck() {
    this.wheel = 6;
    this.beep = "Truck_HONK";
};

Truck.prototype = new Car();

function SUV() {
    this.beep = "SUV_WANK";
}

SUV.prototype = new Car();

var truck = new Truck(),
    suv = new SUV();

truck.wheel	//6
suv.wheel	//4
truck.beep	//Truck_HONK
suv.beep	//SUV_WANK
truck.go();	//Truck_HONK
suv.go();	//SUV_WANK

1) truck 객체에 go 속성이 있는지 검사
2) Truck.prototype(new Car())에 go 속성이 있는지 검사
3) new Car()에 go() 속성이 없으면, new Car()로 생성된 객체의 프로토타입인 Car.prototype에 go
   속성이 있는지 검사
4) Car.prototype.go 속성 참조

프로토타입의 장단점
생성자를 사용해서 객체를 조금만 생성한다면 그냥 속성을 부여하는 것이 낫다.
프로토타입은 모든 객체가 한 객체를 공유하고 있어 메모리를 하나만 사용 따라서 여러개를 생성할 경우
프로토타입을 사용하는 방법이 메모리상 유리하다.

프로토타입 체인을 따라서 검색하는 속성 탐색 시간이 늘어난다.
속성을 탐색할 때, 먼저 해당 객체의 속성인지 탐색하고, 없다면 해당 객체의 constructor.prototype을
탐색하고, 없다면 다시 해당 객체의 프로토타입을 탐색하는 식으로 연쇄적인 속성 탐색이 자바스크립트 엔진에
따라서는 다소 소모적일 수 있기 때문
```
#### 상속
```{.javascript}

* 1) 초창기 자바스크립트 상속 구현 방법
function Person() {
    this.name = "anonymous";
    this.job = "none";
    this.sayHello = function() {
        console.log("Hello, my name is " + this.name);
    };
}

function Unikys() {
    var obj = new Person(); // *Person을 생성해서 반환함
    obj.name = "unikys";
    obj.job = "Programmer";
    return obj;
}

var unikys = new Unikys();
unikys.sayHello();	// "Hello my name is uikys"

unikys instanceof Person	// true
unikys instanceof Unikys	// false (new Unikys로 생성했지만) Unikys의 인스턴스로 인식을
못한다.

* 2) function에 기본으로 들어있는 프로토타입 속성을 새로운 객체로 설정하여 상속하는 방법
앞에서 설명한 프로토타입을 새로운 객체를 선언하듯이, 상속하고자 하는 객체를 하위 객체의 프로토타입
속성으로 설정

var person = {
    name: "anonymous",
    sayHello: function() {
        console.log("Hello, my name is " + this.name);
    }
};	//person 변수를 객체 표현식으로 정의해 객체로 생성

function Unikys() {
    this.name = "Unikys";
}

Unikys.prototype = person;
var unikys = new Unikys();

unikys.sayHello();  // "Hello, my name is Unikys"
person.sayHello();  // "Hello, my name is anomymous"
unikys instanceof Unikys;   // true

instanceof Unikys는 정상으로 true가 나오지만, unikys 변수가 person 변수를 상속했다는 것을
unikys instanceof person과 같은 코드로 확인 할 수 가 없다.

* 3) 프로토타입을 이용한 자바스크립트 상속 구현
function Person() {
    this.name = "anonymous";
    this.sayHello = function() {
        console.log("Hello, my name is " + this.name);
    };
}

function Unikys() {
    this.name = "Unikys";
}

Unikys.prototype = new Person();

var unikys = new Unikys();
unikys.sayHello();

unikys instanceof Unikys;   //true
unikys instanceof Person;   //true

상기의 2번 문제를 해결
```