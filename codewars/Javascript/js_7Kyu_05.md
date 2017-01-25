#7Kyu
##Sum of the first nth term of Series

Your task is to write a function which returns the sum of following series upto nth term(parameter).

Series: 1 + 1/4 + 1/7 + 1/10 + 1/13 + 1/16 +...
Rules:

You need to round the answer upto 2 decimal places and return it as String.
If the given value is 0 then it should return 0.00
You will only be given Natural Numbers as arguments.
Examples:

SeriesSum(1) => 1 = "1"
SeriesSum(2) => 1 + 1/4 = "1.25"
SeriesSum(5) => 1 + 1/4 + 1/7 + 1/10 + 1/13 = "1.57"

###Solution
```{.javascript}
function SeriesSum(n) {
  if (n > 0) {
    var sum = 1;
    var denominator = 4
    for (var i=0; i<n - 1; i++) {
        var val = (1/denominator);
        denominator += 3;
        sum += val;
    }
    return sum.toFixed(2);
  } else {
    return '0.00';
  }
}
```
```{.javascript}
function seriesSum(n) {
    for (var s = 0, i = 0; i < n; i++) {
        s += 1 / (1 + i * 3);
    }
    return s.toFixed(2);
}
```

```{.javascript}
Number.prototype.toFixed();
고정 소수점 표기법을 사용하여 숫자를 반환.

Syntax
numObj.toFixed([digit]);

digit - 선택적 파라미터, 없으면 0으로 간주 digit의 범위는 0~20, 벗어나면 RangeError Exception 발생

Ex)
var numObj = 12345.6789;

numObj.toFixed();       //  '12346': 반올림하며, 소수 부분을 남기지 않음
numObj.toFixed(1);      //  '12345.7': 반올림
numObj.toFixed(6);      //  '12345.678900': 빈 공간을 0으로..
(1.23e+20).toFixed(2);  //  '123000000000000000000.00'
(1.23e-10).toFixed(2);  //  '0.00'
2.34.toFixed(1);        //  '2.3'
2.35.toFixed(1);        //  '2.4'. 이 경우에는 올림
-2.34.toFixed(1);       //  -2.3 (연산자의 적용이 우선이기 때문에, 음수의 경우 문자열로 반환 X)
(-2.34).toFixed(1);     //  '-2.3' (...괄호를 사용할 경우 문자열을 반환.)
```