### JavaScript Memoization 패턴

##### Memoization
>패턴의 이름대로 '메모'를 하는 것이 특징인데, 메모를 하는 대상은 바로 함수 또는 객체이다.
특정 아이템을 검색하려고 할 때, 검색 결과를 ID 기반으로 캐시 처리하는 메모제이션 패턴
기본적으로 계산된 결과를 함수 프로퍼티값으로 담아 놓고 나중에 사용한다.

```javascript
(function () {
    var inputItemId = document.getElementById("itemId");
    function searchItem(id) {
        var xhr;

        if(searchItem.cache.hasOwnProperty(id)) {
            return searchItem.cache[id];
        }

        xhr = new XMLHttpRequest();
        xhr.open("GET", "/searchItem");
        xhr.onload = function () {
            var item = JSON.parse(xrh.responseText);
            searchItem.cache[item.id] = item;
        }
        xhr.send();
    }
    searchItem.cache = {};

    document.getElementsById("search").addEventListener("click", function () {
        searchItem(searchItem.value);
    });
}());

// ---------------------------------------- 피보나치 수열합 예제 ---------------------------------------- //

<body>
<script>
    (function () {
        function fibonacci(n) {
            if (n === 0 || n === 1) {
                return n;
            } else {
                return fibonacci(n - 1) + fibonacci(n - 2);
            }
        }

        var fibonacciMemo = (function () {
            return function (n) {
                var result = fibonacciMemo.memo[n];
                if (typeof result !== 'number') {
                    result = fibonacciMemo(n - 1) + fibonacciMemo(n - 2);
                    fibonacciMemo.meno[n] = result;
                }
                return result;
            };
        }());
        fibonacciMemo.memo = [0, 1];

        var testNum = 40,
            start, end;

        start = Date.now();
        console.log(fibonacci(testNum));
        end = Date.now();
        console.log(`Elapsed time of ${((end - start)/1000).toFixed(2)} + 
        			seconds for recursive fibonacci(${testNum})`);

        start = Date.now();
        console.log(fibonacciMemo(testNum));
        end = Date.now();
        console.log(`Elapsed time of ${((end - start)/1000).toFixed(2)} +
        			seconds for recursive fibonacci(${testNum})`);
    }());
</script>
</body>

// ---------------------------------------- 팩토리얼 예제 ---------------------------------------- //

var fact = function() {
	var cache = {'0': 1};
    var func = function(n) {
    	var result = 0;

        if (typeof(cache[n]) === 'number') {
        	result = cache[n];
        } else {
        	result = cache[n] = n * func(n-1);
        }

        return result;
    }

    return func;
}();

// 앞서 계산한 결과값을 캐쉬에 저장한 뒤 재활용 한다.
console.log(fact(10));
console.log(fact(20));
```