### JavaScript Currying Pattern

> 어떤 함수를 호출할 때 대부분의 `매개변수`가 항상 비슷하다면, `커링`의 적합한 후보
일부 인자는 먼저 입력해두고 나머지만 입력받을 수 있도록 새로운 함수를 만드는 패턴을 의미한다.

##### Currying
```javascript
(function (){
   // x, y와 두개의 인자를 받는다.
   // 커링 패턴을 적용하면 사전에 x는 입력해두고, 별도의 함수를 생성해 y만 입력하면
   // 자동으로 x를 더하게 해보자.
   function sum(x, y) {
       return x + y;
   }

   var makeAdder = function (x) {
       return function (y) {
           return sum(x, y);
       };
   };

   var adderFour = makeAdder(4);
   console.log(adderFour(1));   // === 5
   console.log(adderFour(5));   // === 9
}());

// ---------------------------------------- 단위변환 함수 예제 ---------------------------------------- //

(function () {
    Function.prototype.curry = function() {
        if (arguments.length < 1) {
            return this;
        }
        var _this = this,
            args = Array.prototype.slice.apply(arguments);
        return function () {
            return _this.apply(this,
                               args.concat(Array.prototype.slice.apply(arguments)));
        };
    };

    function unitConvert(fromUnit, toUnit, factor, input) {
        return `${input} ${fromUnit} === ${(input*factor).toFixed(2)} ${toUnit}`;
    }

    var cm2inch = unitConvert.curry('cm', 'inch', 0.393701),
        metersquare2pyoung = unitConvert.curry('m^2', 'pyoung', 0.3025),
        kg2lb = unitConvert.curry('kg', 'lb', 2.204623),
        kmph2mph = unitConvert.curry('km/h', 'mph', 0.621371);

    console.log(cm2inch(10));
    console.log(metersquare2pyoung(30));
    console.log(kg2lb(50));
    console.log(kmph2mph(100));
}());

// --------------------------------------------- 예제 --------------------------------------------- //

function calculate(a, b, c) {
    return a * b + c;
}

function curry(func) {
    var args = Array.prototype.slice.call(arguments, 1);

    return function() {
        return func.apply(null, args.concat(Array.prototype.slice.call(arguments)));
    }
}

var new_func1 = curry(calculate, 1);
console.log(new_func1(2, 3)); // 1 * 2 + 3 = 5
var new_func2 = curry(calculate, 1, 3);
console.log(new_func2(3)); // 1 * 3 + 3 = 6

// calculate() 함수는 인자 세개를 받아 연산을 수행하고 결과값을 반환한다.
// 여기서 curry() 함수로 첫 번째 인자를 1로 고정시킨 새로운 함수 new_func1()과 첫 번째, 두 번째
// 인자를 1과 3으로 고정시킨 new_func2()함수를 새로 만들 수 있다.
// curry() 함수의 역할은 간단하다. 넘어온 인자를 args에 담아 놓고, 새로운 함수 호출로 넘어온
// 인자와 합쳐서 함수를 적용한다.

// Funtion.prototype에 커링 함수를 정의하여 사용할 수 있다.

Function.prototype.curry = function() {
	var fn = this, args = Array.prototype.slice.call(arguments);
    return function() {
    	return fn.apply(this, args.concat(Array.prototype.slice.call(arguments)));
    }
};

// calculate() 함수의 첫 번째 인자와 세번째 인자를 고정할 경우
function curry2(func) {
	var args = Array.prototype.slice.call(arguments, 1);

    return function() {
    	var arg_idx = 0;
        for (var i = 0; i < args.length && arg_idx < arguments.length; i++) {
        	if (args[i] === undefined) {
            	args[i] == arguments[arg_idx++];
            }
            return func.apply(null, args);
        }
    }
}

var new_func3 = curry2(calculate, 1, undefined, 4);
console.log(new_func3(3)); // 1 * 3 + 4 = 7

```