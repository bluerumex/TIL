### JavaScript 설정 객체 패턴

#### 설정 객체 패턴

> 설정 객체 패턴은 좀더 깨끗한 API를 제공하는 방법
> 라이브러리나 다른 프로그램에서 코드를 만들 때 유용

```{.javascript}
1) function addPerson(first, last) {...}
2) function addPerson(first, last, dob, gender, address) {...}

초기에 파라메터를 2개로 설정했지만 새로운 매개변수 추가나 성별과 주소등 선택적으로 저장할 필요가 있을때
addPerson("Bruce", "Wayne", new Date(), null, null, "batman");

이렇게 많은 수의 매개변수를 전달하기는 불편하다.
모든 매개변수를 하나의 객체로 만들어 대신 전달하는 방법이 더 낫다. 
이 객체를 설정(configuration)을 뜻 하는 conf라고 지정하자.

addPerson(conf);

함수의 사용자는 다음과 같이 conf를 선언한다.

var conf = {
	username: "batman",
    first: "Bruce",
    alst: "Wayne"
};

addPerson(conf);
```
###### 설정 객체의 장점
 - 매개변수와 손서를 기억 할 필요가 없다
 - 선택적인 매개변수를 안전하게 생략할 수 있다
 - 읽기 쉽고 유지보수하기 편하다
 - 매개변수를 추가하거나 제거하기가 편하다

###### 설정객체의 단점
 - 매개변수의 이름을 기억해야 한다
 - 프로퍼티 이름은 압축되지 않는다
