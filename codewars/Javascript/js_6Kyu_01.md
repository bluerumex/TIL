#6 kyu
##Counting Duplicates

```
Description:

Count the number of Duplicates

Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits 
that occur more than once in the input string. 
The input string can be assumed to contain only alphanumeric characters, 
including digits, uppercase and lowercase alphabets.

Example

"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabbcdeB" -> 2 # 'a' and 'b'
"indivisibility" -> 1 # 'i'
"Indivisibilities" -> 2 # 'i' and 's'
"aa11" -> 2 # 'a' and '1'
```

###Solution
```{.javascript}
function duplicateCount(text){
    var splitText = [];
    var totalCount = 0;
    var duplicateCnt = 0;

    for (var i=0; i<text.length; i++) {
        var str = text[i].toLocaleLowerCase();
        var idx = splitText.indexOf(str);

        if (idx == -1) {
            splitText.push(str);
        }

    }

    for (var i=0; i<text.length; i++) {
        var str = splitText[i];

        for (var j=0; j<text.length; j++) {
            if (str == text[j].toLocaleLowerCase()) {
                duplicateCnt++;
            }
        }

        if (duplicateCnt >= 2) {
            totalCount++;
        }

        duplicateCnt = 0;
    }

    return totalCount;
}
```
```{.javascrpit}
function duplicateCount(text){
  return (text.toLowerCase().split('').sort().join('').match(/([^])\1+/g) || []).length;
}

```
```
String.prototype.indexOf()

호출한 String객체에서 입력한 파라메터와 일치하는 Index를 반환한다. 일치하는 값이 없으면 -1 return

Syntax
str.indexOf(searchValue[, fromIndex]);
searchValue: 찾고자 하는 문자열
fromIndex(optional) :
문자열에서 찾기 시작하는 위치를 나타내는 인덱스 값, 어떤 정수값이라도 가능 기본값은 0(문자열 전체를 대상으로 함)

fromIndex >= str.length 이면 검색하지 않고 바로 -1 return, searchValue가 공백문자열이 아니라면 str.length를 반환.

indexOf() 대소문자를 구분 b, B 다르게 인식

'Blue Whale'.indexOf('Blue');     // returns  0
'Whale Blue'.indexOf('Blue');	  // returns  6
'Blue Whale'.indexOf('Blute');    // returns -1
'Blue Whale'.indexOf('Whale', 0); // returns  5
'Blue Whale'.indexOf('Whale', 5); // returns  5
'Blue Whale'.indexOf('', 9);      // returns  9
'Blue Whale'.indexOf('', 10);     // returns 10
'Blue Whale'.indexOf('', 11);     // 전체 문자열의 길이가 10이므로, 10을 반환


*indexOf()를 이용한 특정 문자 count
var str = 'To be, or not to be, that is the question.';
var count = 0;
var pos = str.indexOf('e'); //pos는 4의 값을 가짐.

while (pos !== -1) {
  count++;
  pos = str.indexOf('e', pos + 1); // 첫 번째 e 이후의 인덱스부터 e를 찾음
}

console.log(count); // 로그에 4를 출력.
```
```
Array.prototype.sort()
배열의 요소를 적절한 위치에 정렬하고 배열을 반환.
sort는 유니코드 기준으로 오름차순..

Syntax
arr.sort()
arr.sort(compareFunction)

Parameters

compareFunction {{optional_inline}}
정렬 순서를 정의하는 함수를 지정합. 생략하면 배열은 각 요소의 문자열 변환에 따라 각 문자의 유니 코드 코드 포인트 값에 따라 정렬.

compareFunction가 제공되면 배열 요소는 compare 함수의 반환 값에 따라 정렬됩니다. a와 b가 비교되는 두 요소라면,

compareFunction (a, b)가 0보다 작은 경우 a를 b보다 낮은 색인으로 정렬합니다. 즉, a가 먼저

compareFunction (a, b)가 0을 반환하면 a와 b를 서로에 대해 변경하지 않고 모든 다른 요소에 대해 정렬unction (a, b)가 0보다 큰 경우, b를 a보다 낮은 인덱스로 소트.

compareFunction (a, b)는 요소 a와 b의 특정 쌍이 두 개의 인수로 주어질 때 항상 동일한 값을 반환해야한다 일치하지 않는 결과가 반환되면 정렬 순서는 정의되지 않음.

compare함수의 형식
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}

문자열 대신 숫자를 비교하기 위해 compare 함수는 a에서 b를 뺄 수 있습니다. 다음 함수는 배열을 오름차순으로 정렬합니다 (Infinity 및 NaN이 포함되어 있지 않은 경우).

function compareNumbers(a, b) {
  return a - b;
}

```


var scores = [1, 10, 21, 2]; 
scores.sort(); // [1, 10, 2, 21]

10이 2보다 앞선다.. unicode...기준
숫자는 문자열로 변환되어서 값이 결정되어짐.




```