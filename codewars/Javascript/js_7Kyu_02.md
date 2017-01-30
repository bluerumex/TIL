#7Kyu
##Get the Middle Character
```
Description:
You are going to be given a word. Your job is to return the middle character of the word. 
If the word's length is odd, return the middle character. 
If the word's length is even, return the middle 2 characters.

Examples:
Kata.getMiddle("test") should return "es"
Kata.getMiddle("testing") should return "t"
Kata.getMiddle("middle") should return "dd"
Kata.getMiddle("A") should return "A"
```

###Solutions

```{.javascript}
function getMiddle(s) {
  var length = s.length;
  var str = '';
  var divide = Math.round(length / 2);
  if (length % 2 == 0) {
    str = s.substr(divide - 1, 2);
  } else {
    str = s.substr(divide - 1, 1);
  }
  return str;
}
```

###Best Practices

case. 1
```{.javascript}
function getMiddle(s) {
  return s.substr(Math.ceil(s.length / 2 - 1), s.length % 2 === 0 ? 2 : 1);
}
```

case. 2
```{.javascript}
function getMiddle(s) {
  var middle = s.length / 2;
  return (s.length % 2)
    ? s.charAt(Math.floor(middle))
    : s.slice(middle - 1, middle + 1);
}
```


substring, substr 차이

1) substring(startIndex, endIndex);
시작 인덱스와 종료 인덱스를 설정해서 문자열을 반환한다.
종료 인덱스가 없으면 시작 인덱스부터 모든 문자열을 반환한다.

2) substr(startIndex, length);
시작 인덱스를 설정하고, 두번째 매개변수로는 가져올 길이설정.

Math 함수
Math.ceil() : 소수점 올림, 정수 반환
Math.floor() : 소수점 버림, 정수 반환
Math.round() : 소수점 반올림, 정수반환
