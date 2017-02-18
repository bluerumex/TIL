### jQuery 4. Utilities

#### jQuery.extend()
```{.jquery}
jQuery.extend([deep], target [, object1 ] [, objectN ] )

$.extend() 두개 이상의 객체를 합치는 메서드

deep - true 라면, 깊은 수준 복사
target - 합쳐지는 추가 객체의 속성을 받을 객체 또는 유일한 인자일 경우 
	     jQuery 네임스페이스로 확장될 객체
object1 - 합쳐질 때 기준이 될 객체
objectN -  기준 객체에 합쳐질 추가 객체

var object1 = { apple: 0, 
				banana: {weight: 52, price: 100}, 
                cherry: 97 
              }; 
var object2 = { banana: {price: 200}, 
				durian: 100 
              }; /* merge object2 into object1 */ 

$.extend(object1, object2);

결과 : {"apple":0,"banana":{"weight":52,"price":200},"cherry":97,"durian":100}

recursively한 merge

var object1 = { apple: 0, 
				banana: {weight: 52, price: 100}, 
                cherry: 97 
               }; 
var object2 = { banana: {price: 200}, durian: 100 }; 
/* merge object2 into object1, recursively */ 

$.extend(true, object1, object2);

결과 : {"apple":0,"banana":{"weight":52,"price":200},"cherry":97,"durian":100}
```
#### jQuery.each()
```{.javasript}
jQuery.each( array, callback )
jQuery.each( object, callback)

$.each()는 일반적인 반복 작업을 위한 메서드이다.

array - 첫번째 매개변수는 array또는 ojbect
callback - 각각의 요소에 대해 실행될 콜백 메서드

array일 경우 callback(index, value);
object일 경우 callback(key, value); 


$('div').each(function); (첫 번째 매개변수로 콜백 함수를 지정하는 jQuery 컬렉션 메서드와 약간다르다)

function - Type: Function( Integer index, Element element )
                 A function to execute for each matched element.
```
#### jQuery.grep()
```{.javascript}
배열에서 요소를 필터링하고 제거할 필요가 있을때.	

jQuery.grep( array, function [, invert ] )
Returns: Array

array - Type: array like object
function - Type : Function(value, i) // value = 배열의 값, i 루프 증가값
invert - Type : boolean // defalut는 false, function return 결과 참인것만 배열에 추가
                        // true일 경우 return 결과가 false인 결과를 추가
```
#### jQuery.map()
```{.javascript}
배열의 각 요소에 대해 루프를 돌며 그 값을 수정해야 될 때

jQuery.map( array, callback )
Returns: Array

function - Type : Function(value, i) // value = 배열의 값, i 루프 증가값

var arr = [ "a", "b", "c", "d", "e" ];

$.map( arr, function( n, i ) {
  return ( n.toUpperCase() + i );
});
```
#### jQuery.merge()
```{.javascript}
두 개의 배열을 merge할 경우

jQuery.merge( first, second )
Returns: Array

first, secont - Type : Array

$.merge( [ 0, 1, 2 ], [ 2, 3, 4 ] )
결과 : [ 0, 1, 2, 2, 3, 4 ]
```
#### jQuery.makeArray()
```{.javascript}
jQuery와 JavaScript 의 많은 일반적인 함수들은 배열과 비슷한 오브젝트들을 반환한다.
예를 들어, jQuery 함수를 의미하는 $()은 배열로 이루어진 속성들을 지닌 jQuery 객체를 반환한다
이렇게 반환되는 객체들이 정확하게 배열과 같다고 할 수는 없다.

plain Javascript 배열화 한다고 생각하자.
```
#### jQuery.unique()
```{.javascript}
중복된 배열 항목 필터링

```
