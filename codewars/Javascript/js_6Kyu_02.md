#6 kyu
##Counting Duplicates

```
Description:

Given an array (arr) as an argument complete the function 
countSmileys that should return the total number of smiling faces.

Rules for a smiling face:
-Each smiley face must contain a valid pair of eyes. Eyes can be marked as : or ;
-A smiley face can have a nose but it does not have to. Valid characters for a nose are - or ~
-Every smiling face must have a smiling mouth that should be marked with either ) or D.
Valid smiley face examples:
:) :D ;-D :~)
Invalid smiley faces:
;( :> :} :] 

Example cases:

countSmileys([':)', ';(', ';}', ':-D']);       // should return 2;
countSmileys([';D', ':-(', ':-)', ';~)']);     // should return 3;
countSmileys([';]', ':[', ';*', ':$', ';-D']); // should return 1;

```

###Solution
```{.javascript}
function countSmileys(arr) {
    var count = 0;
    for (var i in arr) {
        arr[i].match(/[:;][~-][)D]|[:;][)D]/)!=null?count++:[];
    }
    return count;
}


const countSmileys = ss => ss.reduce((a, s) => a + /^[:;][-~]?[D)]$/.test(s), 0);


function countSmileys(arr) {
  return arr.filter(x => /^[:;][-~]?[)D]$/.test(x)).length;
}


function countSmileys(arr) {
  return arr.reduce((n, s) => /^[:;][-~]?[)D]$/.test(s) ? n + 1 : n, 0)
}

```
<br>
#####RegExp.prototype.test()
```{.javascript}
정규표현식의 test() 메소드는 대상 문자열 속에 일치하는 문자열이 포함되어 있는지 검사하고 
true 또는 false를 반환한다. 

Syntax
regexObj.test(str)

var str = "hello world!";
var result = /^hello/.test(str);
console.log(result); // true


```
<br>
#####Array.prototype.reduce()
```{.javascript}
reduce() 메서드는 누산기(accumulator) 및 배열의 각 값(좌에서 우로)에 대해 (누산된) 
한 값으로 줄도록 함수를 적용합니다.
배열에 조건을 주어 조건에 만족하지 못하는 원소들을 걸러낸다.

Syntax
arr.reduce(callback[, initialValue])

매개변수

callback
    배열의 각 (요소) 값에 실행할 함수, 인수(argument) 4개는:
    previousValue
    이전 마지막 콜백 호출에서 반환된 값 또는 공급된 경우 initialValue. (아래 참조.)
    currentValue
    배열 내 현재 처리되고 있는 요소(element).
    currentIndex
    배열 내 현재 처리되고 있는 요소의 인덱스.
    array
    reduce에 호출되는 배열.
initialValue
선택사항. callback의 첫 호출에 첫 번째 인수로 사용하는 값.


[0, 1, 2, 3, 4].reduce(function(previousValue, currentValue, currentIndex, array) {
    return previousValue + currentValue;
});

콜백은 4번 호출, 다음과 같이 각 호출의 인수 및 반환값과 함께

        previousValue	currentValue	currentIndex	array			반환값
1번째 호출		0				1			1		[0, 1, 2, 3, 4]	1
2번째 호출		1				2			2		[0, 1, 2, 3, 4]	3
3번째 호출		3				3			3		[0, 1, 2, 3, 4]	6
4번째 호출		6				4			4		[0, 1, 2, 3, 4]	10

[0, 1, 2, 3, 4].reduce( (prev, curr) => prev + curr );
위와 같은 동일한 결과 리턴

*initialValue 설정시
[0, 1, 2, 3, 4].reduce(function(previousValue, currentValue, currentIndex, array) {
  return previousValue + currentValue;
}, 10);

 		previousValue	currentValue	currentIndex	array			반환값
1번째 호출		10				0			0		[0, 1, 2, 3, 4]	10
2번째 호출		10				1			1		[0, 1, 2, 3, 4]	11
3번째 호출		11				2			2		[0, 1, 2, 3, 4]	13
4번째 호출		13				3			3		[0, 1, 2, 3, 4]	16
5번째 호출		16				4			4		[0, 1, 2, 3, 4]	20
```
<br>
#####Array.prototype.filter()
```{.javascript}
filter() 메소드는 제공된 함수로 구현된 테스트를 통과하는 모든 요소가 있는 새로운 배열을 만든다.

Syntax
var new_array = arr.filter(callback[, thisArg])

매개변수

callback
    배열의 각 요소를 테스트하는 함수. 인수 (element, index, array) 와 함께 호출됨. 
    요소를 (새 배열에) 계속 두기 위해 true를 반환, 그렇지 않으면 false.
    thisArg
    선택 사항. callback을 실행할 때 this로 사용하는 값.

반환값
테스트를 통과한 요소가 있는 새로운 배열.

function isBigEnough(value) {
  return value >= 10;
}
var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
// filtered 는 [12, 130, 44]

```


