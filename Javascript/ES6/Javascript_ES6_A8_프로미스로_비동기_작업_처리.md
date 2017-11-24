### ECMA Script 6

>ECMAScript 6 문법

##### A.8 프로미스로 비동기 작업 처리하기
```javascript
// A.8.1 콜백 지옥(callback hell)
// 기존에 비동기 작업을 처리할 때 보통 콜백을 사용했는데, A함수를 실행하며서 다음에 실행할 함수 B를 인자로 전달하고,
// 함수 A의 실행이 끝나면 함수 A가 B를 실행하는 방식이였다.
// 이런식의 비동기 로직이 중첩되어 있다면 가독성도 심각할 것이다.


// A.8.2 프로미스(Promises)
// Promise 객체는 비동기 작업이 끝나기를 기다렸다가 작업의 결과에 따라 다음 작업을 진행할지, 에러를 처리할지 결정하며,
// 이 동작을 구현하기 위해 Promise 객체는 다음 중 하나의 상태로 존재한다.
1) Fulfilled : 작업이 성공한 경우
2) Rejected: 작업이 실패한한 경우, 에러를 반환
3) Pending: 작업이 아직 진행 중인 경우

// Promise 객체는 생성하면서 생성자에 두 함수를 전달하는데, 순서대로 fulfilled 상태가 될 때 실행될 함수와
// rejected 상태가 될 때 실핼될 함수다.

function getCustomers() {
    return new Promise (
        function(resolve, reject) {
            console.log('Getting customers');

            // 서버 응답을 setTimeout() 함수로 대신한다.
            setTimeout(function() {
                var success = true;
                if (success) {
                    resolve("John Smith");
                } else {
                    reject(`Can't get customers`);
                }
            }, 1000);
        }
    )
}

let promise = getCustomers()
    .then((cust) => console.log(cust))
    .catch((err) => console.log(err));
console.log('Invoked getCustomers. Waiting for results');

// getCustomer() 함수는 처리되는 결과에 따라 resolve() reject() 함수를 실행하는데,
// 두 함수 모두 Promise 객체를 반환한다. 다만 resolve() 함수는 fulfilled 상태의 Promise객체를 반환하고,
// reject() 함수는 rejected 상태의 Promise 객체를 반환한다.
// getCustomer() 함수에서 resolve('John Smith')가 실행되어 fulfilled 상태의 Promise 객체가 반환되며 then() 함수가 실행되면서,
// "John Smith"를 cust 인자로 받을 것이다

```