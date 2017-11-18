### ECMA Script 6

>ECMAScript 6 문법

##### A.6 forEach(), for-in, for-of 컬렉션을 순회하는 API
```javascript
// A.6.1 forEach()
var numberArray = [1,2,3,4];
numberArray.description = 'four numbers';

numberArray.forEach((n) => console.log(n)); // 1, 2, 3, 4

// forEach() 함수는 배열을 순회하며서 각 항목을 인자로 받아 콜솔에 출력히자만,
// 배열에 있는 description 프로퍼티는 무시된다.
// 그리고 forEach() 함수는 중간에 멈출 수 없으며, 조건에 따라 중간에 멈춰야 한다면 forEach대신 every() 를 사용해야된다.


// A.6.2 for-in
// for-in 루프는 객체의 프로퍼티 이름을 순회하거나 배열과 같은 데이터 컬렉션을 순회할 수 있다.
// Javascript에서 객체는 키-값 컬렉션이며, 프로퍼티의 이름과 값은 여기에 해당된다.
// 위쪽 numberArray 재활용, 루프를 순회하면 5개의 프로퍼티로 처리된다.

for (let n in numberArray) {
    console.log(n);
    // 0, 1, 2, 3 description
    // 개발자 도구를 열어보면 프로퍼티 이름이 문자열로 출력되는 것을 확인할 수 있다.
}

// 값을 확인할면 객체의 값을 참조해서 numberArray[n] 형식으로 사용한다.
for (let n in numbersArray) {
    console.log(numberArray[n]);
    // 1, 2, 3, 4, for numbers
}

// forEach() 함수는 컬렉션에 있는 데이터만 순회하지만, for-in 루프는 컬렉션 데이터와 프로퍼티 모두 순회한다.
// 이 동작은 프로퍼티 전부를 사용할때는 적합하지만, 배열의 각 항목을 순회하는 일반적인 용도로 사용한다면 주의해야된다.



```


