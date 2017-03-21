### JavaScript currying 패턴

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

```