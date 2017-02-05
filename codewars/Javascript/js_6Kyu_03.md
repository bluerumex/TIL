#6 kyu
##The maximum sum value of ranges -- Simple version

```
Description:

Given an array arr that contains some integers(positive, negative or 0), 
and a range list such as [[start1,end1],[start2,end2],...], 
start and end are the index of arr and start always less than end. 
Your task is to calculate the sum value of each range, and return the maximum sum value.

For example:

Given arr = [1,-2,3,4,-5,-4,3,2,1], 
     range = [[1,3],[0,4],[6,8]]
should return 6

calculation process:
range[1,3] = arr[1]+arr[2]+arr[3] = 5
range[0,4] = arr[0]+arr[1]+arr[2]+arr[3]+arr[4] = 1
range[6,8] = arr[6]+arr[7]+arr[8] = 6
So the maximum sum value is 6

Note:

arr always has at least 5 elements;
range always has at least 1 elements;
All inputs are valid;
This is a simple version, if you want some challenge, please try the challenge version.
Some Examples

maxSum([1,-2,3,4,-5,-4,3,2,1],[[1,3],[0,4],[6,8]]) === 6
maxSum([1,-2,3,4,-5,-4,3,2,1],[[1,3]]) === 5
maxSum([1,-2,3,4,-5,-4,3,2,1],[[1,4],[2,5]]) === 0

Tag : FUNDAMENTALS
```

###Solution
```{.javascript}
function maxSum(arr,range){
    var sumArr = [];
    for (var i in range) {
        var sum = 0;
        var t = range[i];
        var stIdx = t[0];
        var edIdx = t[1];

        for(var st=stIdx; st<=edIdx; st++) {
            sum += arr[st];
        }
        sumArr.push(sum);
    }
    return Math.max.apply(null, sumArr);
}


function maxSum(arr,range){
  return Math.max(...range.map(i => arr.slice(i[0], i[1] + 1).reduce((a, b) => a + b)))
}


function maxSum(arr,range){
  let s = [];
  for(let r of range) {
    s.push(arr.slice(r[0],r[1]+1).reduce((x,y)=>x+y));
  }
  return Math.max(...s);
}
```
<br>
#####Array.prototype.map()
```{.javascript}
map() 메소드는 배열 내의 모든 요소 각각에 대하여  제공된 함수(callback)를 호출하고, 
그 결과를 모아서,  새로운 배열을 반환.

Syntax
arr.map(callback[, thisArg])

파라미터

callback
    새로운 배열 요소를 생성하는 함수로 다음 세 가지 인수를 가집니다.
    currentValue
    배열의 요소 중, 현재 처리되고 있는 요소
    index
    현재 처리되는 요소의 배열 내 인덱스
    array
    map 메소드가 적용되는 본래 배열
thisArg
선택항목. callback을 실행할 때 this로 사용되는 값. 기본값은 Window 객체.


var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots의 값은 [1, 2, 3]이 되지만, numbers는 그대로 [1, 4, 9]입니다.
```


