### Java 1. Exception

예외는 프로그램의 실행 중에 발생하는 이벤트로서 프로그램의 정상적인 실행 흐름을 중단시킨다.
<br>
메소드 안에서 오류가 발생하면 메소드는 발생된 오류를 설명하는 객체를 생성하고 자바 런타임 시스템으로 이 객체를 넘긴다. 이 객체는 예외 객체라고 불리며 오류의 타입과 오류 발생 시의 프로그램의 상태 등의 정보를 포함하고 있다.
<br>
예외가 발생하는 즉시 프로그램이 종료되고, 예외가 발생한 지점 이후의 문장들은 실행되지 않는다.
<br>
catch블록을 사용할때는 범위가 작은것에서 큰것으로 작성해서 사용해야한다.
finally 블록은 예외가 발생했을시 try 블록이 끝나면 무조건 실행된다. return문을 만나도 finally블록이 실행된 다음에 메소드를 빠져나간다.

```{.java}
try {
	out = new PrintWriter(...);
} catch (IOException e) {
	throw new RuntimeException(e);
}
out.close()

예외가 발생하면 자원이 반납되지 않을 수 가 있다.

try {
	out = new PrintWriter(...);
} catch (IOException e) {
	throw new RuntimeException(e);
} finally {
	out.close();
}

예외가 발생하더라도 확실하게 자원이 반납된다.
```
___
**예외의 종류**
<br>
<img src="../img/Exception-Class.png">
모든 예외는 Throwble 클래스로부터 상속되어서 Error와 Exception이라고 하는 두 개의 클래스로 나누어진다. 
<br>
예외에는 Error, RuntimeException, 기타 예외 3종류가 있다.<br>
**Error** - 자바 가상 기계 안에서 치명적인 오류가 발생하면 생성된다. 하드웨어의 오류로 인하여 파일을 읽을 수 없는 경우등.. 이런 경우 IOException발생한다. 애플리케이션은 이러한 Error를 잡아서 사용자에게 보고는 가능하지만 다 이상 처리 할 수는 없다. Error는 예외 처리 대상이 아니다.
<br>
**RuntimeException** - 이들은 주로 프로그래밍 버그나 논리 오류에서 기인한다. 예로 FIleReader 생성자로 전달하는 과정에서 논리 오류로 항상 null값을 전달한다면 생성자는 NullPointerException을 발생한다.
Error와 RuntimeException은 비체크예외(unchecked exception)이라 한다.
<br>
**Error와 RuntimeException**을 제외한 나머지 예외 - 체크(checked) 예외, 컴파일러가 예외를 처리했는지 확인한다. 하지 않았다면 컴파일 오류가 발생.
<br>
___
**예외와 메소드**
==예외를 잡아서 그 자리에서 처리하는 방법==: try-catch블록을 사용하여서 예외를 잡고 처리한다.
<br>
==메소드가 예외를 발생시킨다고 기술하는 방법==: throws를 사용하여, 다른 메소드한테 예외 처리를 맡긴다.