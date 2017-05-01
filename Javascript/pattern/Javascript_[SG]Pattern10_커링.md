### JavaScript currying 패턴

#### summary
> 어떤 함수를 호출할 때 대부분의 `매개변수`가 항상 비슷하다면, `커링`의 적합한 후보
> 

#### currying
```{.javascript}
커링패턴은 함수를 설계할 때 인자 전체를 넘겨서 호출할 수도 있지만, 일부 인자는 먼저 입력해두고
나머지만 입력받을 수 있도록 새로운 함수를 만드는 패턴을 의미한다.

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

단위 변환함수 예제

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

```