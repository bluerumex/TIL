### JavaScript String Methods
```{.javascript}
 
```
#### String.prototype.indexOf()
```{.javascript}
호출한 String객체에서 입력한 파라메터와 일치하는 Index를 반환한다. 일치하는 값이 없으면 -1 return

Syntax
  - str.indexOf(searchValue[, fromIndex]);
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
#### String.prototype.repeat();
```{.javascript}
문자열을 count 만큼 반복한다.

Syntax
  - str.repeat(count);

Parameter
  - count
    (음수일 경우 예외가 발생)
    
'abc'.repeat(-1);   // RangeError
'abc'.repeat(0);    // ''
'abc'.repeat(1);    // 'abc'
'abc'.repeat(2);    // 'abcabc'
'abc'.repeat(3.5);  // 'abcabcabc' (count will be converted to integer)
'abc'.repeat(1/0);  // RangeError
```
