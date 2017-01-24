### Java 3. Generic

Generic은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법을 말한다.
<br>또한 하나의 코드를 여러 타입에 대하여 재사용할 수 있도록 해주는 기술 중 하나이다.
<br>
```{.java}
public class Box<T> { //T는 타입을 의미한다.
	private T data;
    public void set(T data) {
    	this.data = data;
    }
    public T get() {
    	return data;
    }
}

Box<String> b = new Box<String>();
Box<Integer> b = new Box<Integer>();

Box<String> b = new Box<>();
Box 클래스에 저장하는 데이터 타입은 객체 생성시 결정.
자바 7버전 부터는 생성자 호출시 구체적인 타입을 명시하지 않아도 된다.

//제네릭에는 기본형 타입은 사용할 수 없다.
int -> Integer wrapper class를 사용해야한다.
```
**타입 매개변수의 표기(관례적)**
<br>
E - Element(요소: 자바 컬렉션 라이브러리에서 많이 사용)<br>
K - Key<br>
N - Number<br>
T - Type<br>
V - Value<br>
S, U, V 등 - 2번째, 3번째, 4번째 타입
<br>
<br>
**제네릭 메소드**<br>
```{.java}
<T, R> R method(T t)
제네릭 메소드를 선언하는 방법은 리턴 타입 앞에<> 기호를 추가하고 타입 파라미터를 기술한 다음,
리턴 타입과 매개타입으로 타입 파라미터를 사용하면 된다.

public <T> Box<T> boxing(T t) { ... }
Box<Integer> box = <Integer> boxing(100);

public <U> void printInfo(U info) {
	system.out.println(into);
}
```