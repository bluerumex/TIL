### JavaScript Scope, Closure

#### Scope	
```{.javascript}
다른 언어와 달리 일반적인 블록 스코프를 따르지 않음

<script>
    for (var i = 0; i < 10; i++) {
        var total = (total || 0 )  + i;
        var last = i;
        if (total > 16) {
            break;
        }
    }
</script>

console.log(typeof total !== 'undefined'); // true
console.log(typeof last !== 'undefined'); // true
console.log(typeof i !== 'undefined'); // true
total === 21, last === 6
total, last, i 값에 접근가능함 // global..

블록 스코프를 생성하는 구문
* function
* with
* catch


```