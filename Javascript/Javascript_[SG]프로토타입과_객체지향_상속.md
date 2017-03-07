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
```