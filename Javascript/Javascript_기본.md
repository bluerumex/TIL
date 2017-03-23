### JavaScript 기본.

#### 변수
```{.javascript}
매개변수 전달

ECMASCRIPT의 함수 매개변수는 모두 값으로 전달된다.
매개변수를 값 형태로 넘기면 해당 값은 지역 변수에 복사된다. 즉 이름이 붙은 매개변수로 복사되며
ECMAScript에서는 arguments 객체의 한자리를 차지하게 된다.

function addTen(num) {
	num += 10;
    return num;
}

var count = 20;
var result = addTen(count);
alert(count);	//20 - 변동없음
alert(result);	//30

*참조값 역시 값으로 전달된다.

function setName(obj) {
    obj.name = "Nicholas";
}

var person = new Object();
setName(person);
console.log(person.name); // Nicholas

person객체를 setName() 함수에 넘기면 함수는 해당 객체를 obj에 복사한다.
함수 내부에서는 obj와 person이 모두 같은 객체를 가리킨다.
결과적을 obj는 함수에 값 형태로 전달되었지만 참조를 통해 객체에 접근
함수 내부에서 obj객체에 name 프로퍼티를 추가하면 함수 외부의 객체에도 반영되는데 obj가 가리키는 것은
Heap에 존재하는 전역 객체이기 때문이다.


function setName2(obj) {
    obj.name = "Nichoals";
    obj = new Object();
    obj.name = "Greg";
}

var person = new Object();
setName2(person);
console.log(person.name); // Nicholas

person이 참조로 전달됐다면 person이 가리키는 객체는 자동으로 name프로퍼티가 "Greg"인 새 객체로
변경되어야 한다. 하지만 person.name의 결과는 Nicholas
함수에 값을 전달했기 때문에 함수 내부에서 매개변수의 값이 바뀌었음에도 불구하고 원래 객체에 대한 참조를
그대로 유지. 함수 내부에서 obj를 덮어쓰면 obj는 지역 객체를 가리키는 포인터가 된다. 이 지역객체는
함수가 실행을 마치는 즉시 파괴된다
```
#### 유사배열객체
```{.javascript}
일반 객체에 length 프로퍼티를 가진 객체를 유사배열객체(array-like objects)이라고 한다.
*유사배열객체의 가장 큰 특징은 객체임에도 자바스크립트의 표준 배열 메서드를 사용하는게 가능하다(ex arguemnts)

var arr = ['bar'];
var obj = {
	name: 'foo',
    length: 1	//length 설정
}

arr.push('baz')	// ['bar', 'baz']
obj.push('baz')	// VM685:1 Uncaught TypeError: obj.push is not a function

Array.prototype.push.apply(obj, ['baz']);
// {'1': 'baz', name: 'foo', length: 2}
```