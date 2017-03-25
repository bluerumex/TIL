### JavaScript Array Methods
```{.javascript}
배열은 자바스크립트의 객체의 특별한 형태
배열리터럴 ([])를 사용

*특징
 - 1) 값을 순차적으로 넣을 필요 없이 아무 인덱스 위치에 값을 동적으로 추가 가능
 - 2) 배열 역시 객체다 하지만 약간의 차이가 있다.
 - 3) 배열도 객체이므로 프로퍼티를 동적으로 생성할 수 있다.
 - 4) 유사배열객체

1) 배열의 length 프로퍼티
length property는 배열의 가장 큰 Idexd에 +1을 더 한 값이다.
배열의 length가 3인 배열에 임의로 length를 5를 정의 하면 나머지 인덱스에는 undefined가 할당된다.
(배열의 index 100에 값을 설정했을때 length가 100로 늘어난다 하지만 실제 메모리는 length처럼 할당X)
반대로 length를 줄이게 되면 실제 값은 삭제된다(삭제된 index에는 undefined가 할당)
#undefined 실제 메모리가 할당되지는 않음.

2) 배열과 일반객체의 차이
typeof fooArr	// object (not array), intanceof Array로 타입확인하는 것도 한가지 방법.
typeof fooOjb	// object

일반 객체의 prototype과 배열의 prototype
객체 __prototype__ >> Object.prototype
배열 __prototype__ >> Arraay.prototype >> Object.prototype

length 프로퍼티의 존재 여부 (일반객체에는 length 프로퍼티 X)

3) fooArr.color = "blue", fooArr.name = "arr"
상기방법으로 동적으로 프로퍼티를 추가할 수 있다.
#property를 추가했다고 length가 바뀌는건 아니다. 배열의 length는 배열 원소의 가장 큰 인덱스가 변경 했을때만 변경

4) 유사배열객체
일반 객체에 length 프로퍼티를 가진 객체를 유사배열객체(array-like objects)이라고 한다.
#유사배열객체의 가장 큰 특징은 객체임에도 자바스크립트의 표준 배열 메서드를 사용하는게 가능하다(ex arguemnts)

var arr = ['bar'];
var obj = {
	name: 'foo',
    length: 1	//length 설정
}

arr.push('baz')	// ['bar', 'baz']
obj.push('baz')	// VM685:1 Uncaught TypeError: obj.push is not a function

Array.prototype.push.apply(obj, ['baz']);
// {'1': 'baz', name: 'foo', length: 2}


++
배열의 프로퍼티 열거시 주의
일반 객체는 for in 문으로 프로퍼티를 열거를 해도 되지만, 배열의 경우 for in문은 배열내 불 필요한 프로퍼티가
출력 될 수 있으므로 for문을 사용하는 것이 좋다.

++
배열 요소 삭제
배열도 객체이므로 배열 요소나 프로퍼티를 삭제하는데 delete 연산자를 사용할 수 있다.

delete fooArr[2];	// 2번 인덱스의 해당 값을 undefined로 설정해버린다. length값은 변동(X)
때문에 보통 배열에서 요소를 삭제할 때 splice() 배열 메서드를 사용한다.
#splice(startIndex, deleteCount, item)	// item 삭제할 위치에 추가할 요소

 
```
##### String.prototype.indexOf()
```{.javascript}
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
##### Array.prototype.sort()
```{.javascript}
배열의 요소를 적절한 위치에 정렬하고 배열을 반환.
sort는 유니코드 기준으로 오름차순..

Syntax
arr.sort()
arr.sort(compareFunction)

Parameters
compareFunction {{optional_inline}}
정렬 순서를 정의하는 함수를 지정합. 생략하면 배열은 각 요소의 문자열 변환에 따라
각 문자의 유니 코드 코드 포인트 값에 따라 정렬.

compareFunction가 제공되면 배열 요소는 compare 함수의 반환 값에 따라 정렬
a와 b가 비교되는 두 요소라면,

compareFunction (a, b)가 0보다 작은 경우 a를 b보다 낮은 색인으로 정렬합니다.
>> 배열내 a가 b보다 앞서야 될 경우 0 보다 작은 수가 리턴 되어야 된다.
>> 배열내 a가 b보다 뒤에 있어야 될 경우 0 보다 큰 수가 리턴
>> 0이 return 될 경우 자리 변경 X 

compareFunction (a, b)는 요소 a와 b의 특정 쌍이 두 개의 인수로 주어질 때 
항상 동일한 값을 반환해야한다 일치하지 않는 결과가 반환되면 정렬 순서는 정의되지 않음.

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

문자열 대신 숫자를 비교하기 위해 compare 함수는 a에서 b를 뺄 수 있다
다음 함수는 배열을 오름차순으로 정렬 (Infinity 및 NaN이 포함되어 있지 않은 경우).

function compareNumbers(a, b) {
  return a - b;
}

```
##### Array.prototype.join()
```{.javascript}
join() 메서드는 배열의 모든 요소를 연결해 하나의 문자열로 만든다.

Syntax
str = arr.join([separator = ','])

separator는 optional, 배열의 각 요소를 구분할 문자열을 지정. 
이 구분자는 필요한 경우 문자열로 변환. 생략하면 배열의 요소들이 쉼표로 구분
separator가 빈 문자열이면 모든 요소들이 사이에 아무 문자도 없이 연결.


모든 배열 요소가 문자열로 변환된 다음 하나의 문자열로 연결
값이 undefined이거나 null인 요소는 빈 문자열로 변환

var a = ['바람', '비', '불'];
var myVar1 = a.join();      // myVar1에 '바람,비,불'을 대입
var myVar2 = a.join(', ');  // myVar2에 '바람, 비, 불'을 대입
var myVar3 = a.join(' + '); // myVar3에 '바람 + 비 + 불'을 대입
var myVar4 = a.join('');    // myVar4에 '바람비불'을 대입
```
#### Array.prototype.slice()
```{.javascript}
slice() 메소드는 어떤 배열의 일부에 대한 얇은 복사본 배열을 반환

문법
arr.slice([begin[, end]])

인자
begin
추출을 시작할 zero-based 인자
음수 인덱스는 배열의 끝부터 거리를 나타낸다
slice(-2)는 배열에서 마지막 두 개의 원소를 추출

begin 인자가 undefined인 경우에는, 0번 인덱스부터 시작
end
추출을 종료 할 0 기준 인덱스입니다. 슬라이스는 끝을 제외하고 추출

slice (1, 4)는 네 번째 요소 (1, 2 및 3을 인덱싱 한 요소)를 통해 두 번째 요소를 추출
부의 인덱스로서, end는 순서의 마지막으로부터의 오프셋 (offset)를 나타낸다 
slice (2, -1)는 순서의 두 번째 - 마지막 요소를 통해 세 번째 요소를 추출.
end가 생략되면 slice는 시퀀스의 끝 부분 (arr.length)을 통해 추출
Return value는 추출 된 요소가 포함 된 새로운 배열

var arr = ["a", "b", "c", "d", "e"];

arr.slice(0, 1);	// ["a"];
arr.slice(1, 4);	// ["b", "c", "d"];

end 인덱스는 제외하고 추출한다.
```
#### Araay.prototype.map()
```{.javascript}
map() 메소드는 배열 내의 모든 요소 각각에 대하여  제공된 함수(callback)를 호출하고, 
그 결과를 모아서, 기존 배열은 값은 변형되지 않고 새로운 배열을 반환, 단 callback함수로 인해
변형되 수 도 있음.

문법
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


```
```{.javascript}
String.prototype.match()
일치하는 문자가 있으면 배열로 반환한다.

Syntax
str.match(regexp)
```




