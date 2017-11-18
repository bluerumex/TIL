### ECMA Script 6

>ECMAScript 6 문법

##### A.7 클래스와 상속
```javascript
// ES3, ES5에서도 객체 기반 프로그래밍과 상속을사용할 수 있었다.
// 다만 클래스와 상속을 직접 구현하거나, 서드 파티 라이브러리를 사용해야 했다.
// 이제는 ES6에 클래스 문법이 정식으로 도입되었다.

function Tax() {
    // Tax 객체에서 사용하는 코드
}

function NJTax() {
    // New Jersey Tax 객체에서 사용하는 코드
}

NJTax.prototype = new Tax(); // NJTax가 Tax를 상속받도록 prototype으로 연결한다.
var njTax = new NJTax();

// ES6 Java나 C#과 같은 객체 기반 언어에서 사용하는 class 키워드와 extends 키워드를 도입했다.
// 클래스 선언은 호이스팅되지 않는다. 클래스는 스크립트의 제일 위에 선언되어야 한다.
class Tax {
    // ...
}

class NJTax extends  Tax {
    // ...
}
var njTax = new NJTax();

// ES5 인스턴스 만들기
var tax1 = new Tax(); // Tax 객체의 첫 번째 인스턴스
var tax2 = new Tax(); // Tax 객체의 두 번재 인스턴스

// tax1과 tax2는 Tax클래스에 있는 프로퍼티와 메소드를 사용할 수 있지만, 별개의 인스턴스로 존대한다.
// 프로퍼티가 저장되는 인스턴스가 다르기 때문이다.
// ES5에서는 인스턴스를 새로 만들면 메소드가 중복되어 비효율적인 면이 있었고,
// 코드의 중복을 줄이기 위해 클래스 안에 함수를 정의하지 않고 프로토타입에 정의하는 방법을 사용했다.

function Tax() {
    // ...
}

Tax.prototype = {
    calcTax: function() {
        // 세금을 계산하는 코드
    }
}

// ES6에서도 위 방법도 여전히 유효하지만 문법은 좀 더 편해졌다.
class Tax() {
    calcTax() {
        // 세금을 계산하는 코드
    }
}

// ** 클래스 멤버 변수는 지원하지 않는다 **
// TypeScript는 클래스 멤버 변수를 지원하니 ES6의 클래스와 TypeScript의 클래스의 차이점에 주의하자.
class Tax() {
    var income;
}


// A.7.1 생성자
// 클래스의 constructor() 메소드는 다른 메소드와 용도가 다른 함수이며, 객체의 인스턴스가 만들어질 때 딱 한 번만 실행된다.

class Tax {
    constructor(income) {
        this.income = income;
    }
}

class NJTax extends Tax {
    //...
}

var njTax = new NJTax(5000);
console.log(`The income in njTax instance is ${njTax.income}`);

// NJTax 클래스에 따로 생성자를 정의하지 않았기 때문에 부모 클래스인 Tax 클래스에 있는 생성자가 자동으로 실행된다.
// 자식 클래스에 생성자를 정의한 경우에는 부모 클래스의 생성자가 항상 실행되는 것은 아니며,
// 이 내용은 A.7.4절 super 키워드를 사용할 때 다시 알아본다.


// A.7.2 정적변수(static variables)
// 클래스 프로퍼티 중 여러 객체가 함께 공유하는 프로퍼티가 필요하다면 정적 변수를 만들어 사용할 수 있다.
// 정적 변수는 클래스 선언 밖에서 정의하며, 클래스 A의 counter 프로퍼티를 정적 변수로 만들어
// 모든 A 인스턴스가 공유하고 싶다면 다음과 같이 사용한다.

class A {}
A.counter = 0;

var a1 = new A();
A.counter++;
console.log(A.counter) // 1

var a2 = new A();
A.counter++;
console.log(A.counter) // 2

// 정적 변수는 new 키워드로 만든 인스턴스에 연결되지 않은 것에 주의
// a1 변수를 초기화한 후에 a1 객체를 확인해보면 counter 프로퍼티가 선언되어 있지만 값은 NaN으로 할당되어 있다.
// 정적 변수는 원래 클래스를 통해 접근해야 한다.


// A.7.3 getter, setter, 메소드 정의


```