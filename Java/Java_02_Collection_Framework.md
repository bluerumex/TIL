###  Java 2. Collection Framework

<img src="../img/2160.png" />

<img src="../img/java-util-collection.gif" />

자바 컬렉션 프레임워크는 같은 타입의 객체들을 모아서 담아두는 자바 API 클래스들의 모음이다.
<br>
컬렉션에 포함되어 있는 각 클래스마다 객체를 담거나 꺼내는 메소드를 제공하며 기본적으로 Set, Map, List등 3가지 유형으로 분류할 수 있다.
<br>
Set은 중복된 객체를 넣을 수 없고, Map은 키(Key)와 값(value)의 쌍(pair)을 담는다. List는 객체를 순서대로 담을 수 있으면서 중복된 객체를 담을 수 있다.(Set은 저장된 객체에 순서를 부여하지 않는다.)

| 인터페이스	| 특징|
|------|------|
|List|  *순서가 있는 데이터의 집합 데이터의 중복 허용  <br>데이터를 넣으면 순차적으로 데이터가 들어간다. 각각의 저장되어 있는 공간들은 고유한 인덱스를 갖는다. |
|Set(집합)|  *순서를 유지하지 않는 데이터의 집합, 데이터의 중복을 허용하지 않는다 <br>수학적 개념으로 집합 데이터가 순서와 상관없이 add된다. |
|Map| Key, Value 쌍으로 이루어진 데이터의 집합 순서는 유지되지 않으며<br>Key는 중복을 허용하지 않으나 Value는 중복을 허용한다.|
<br>
```{.java}
    HashSet<Integer> A = new HashSet<Integer>();
    A.add(1);
    A.add(2);
    A.add(3);

    HashSet<Integer> B = new HashSet<Integer>();
    B.add(3);
    B.add(4);
    B.add(5);

    HashSet<Integer> C = new HashSet<Integer>();
    C.add(1);
    C.add(2);

    System.out.println(A.containsAll(B)); // false
    System.out.println(A.containsAll(C)); // true

    //A.addAll(B); 합집합
    //A.retainAll(B); 교집합
    //A.removeAll(B); 차집합
```
<br>
**Iterator 반복자**
Collection 인터페이스의 필드로 정의되어있다.
```{java}
HashSet<Integer> A = new HashSet<Integer>();
A.add(1);
A.add(2);

Iterator itr = A.iterator();
while(itr.hasNext()) {
	System.out.println(itr.next());
}
```
Map 열거 하고자 할때
```{.java}
     
    static void iteratorUsingForEach(HashMap map){
        Set<Map.Entry<String, Integer>> entries = map.entrySet();
        for (Map.Entry<String, Integer> entry : entries) {
            System.out.println(entry.getKey() + " : " + entry.getValue());
        }
    }
     
    static void iteratorUsingIterator(HashMap map){
        Set<Map.Entry<String, Integer>> entries = map.entrySet();
        Iterator<Map.Entry<String, Integer>> i = entries.iterator();
        while(i.hasNext()){
            Map.Entry<String, Integer> entry = i.next();
            System.out.println(entry.getKey()+" : "+entry.getValue());
        }
    }
```