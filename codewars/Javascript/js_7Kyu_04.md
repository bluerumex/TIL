#7Kyu
##Simple Fun #20: First Reverse Try

Given an array arr, swap its first and last elements and return the resulting array.
Example

For arr = [1, 2, 3, 4, 5], the output should be [5, 2, 3, 4, 1]

###Solutions
```{.java}
function firstReverseTry(arr) {
  if (arr.length == 0) {
    return arr;
  } else {
      var reverseArr = arr;
      var idx = arr.length - 1;
      
      var firstNum = arr[0];
      var lastNum = arr[idx];
      
      reverseArr[0] = lastNum;
      reverseArr[idx] = firstNum;
    return reverseArr;
  }
}
```
```{.javascript}
function firstReverseTry(arr) {
  return arr.length < 2 ? arr : [arr[arr.length-1]].concat(arr.slice(1,-1).concat(arr[0]));
}
```
<br>
**slice** - 부분 배열을 반환한다.<br>
slice(first, last); 전달인자를 2개 받음<br>
전달인자가 음수면 우측(마지막 원소)으로 부터 앞쪽으로 전달인자 만큼 위치한 원소를 가리킴<br>
```{.javascript}
var a = [1,2,3,4,5];
a.slice(0,4); // [1,2,3,4]
a.slice(3); // [4,5]
a.slice(-2, -1); // [4]
```