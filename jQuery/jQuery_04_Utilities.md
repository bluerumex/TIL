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