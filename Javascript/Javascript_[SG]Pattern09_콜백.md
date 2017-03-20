### JavaScript callback 패턴

#### callback
```{.javascript}
자바스크립트는 함수 기반으로 동작하기 때문에 이벤트 기반으로 동작하는 부분들은 콜백 함수를 통해서
다양하게 동작하고 있다.

(function () {
    function ajax(method, url, data, callback) {
        var xhr = new XMLHttpRequest();
        xhr.open(method, url);
        xhr.onload = function () {
            if (xhr.status === 200) {
                callback.call(this, xhr.responseText);
            }
        }
        xhr.send(data);
    }

    ajax("POST", "/login", "id=hello&password=world", function (responseText) {
        if (resonseText === "Success") {
            alert("Success to login!");
            ajax("GET", "/userInfo", "id=hello", displayUserInfo);
        } else {
            alert("Failed to login");
        }
    });

    function displayUserInfo() {
        document.getElementById("userInfo").innerHTML = responseText;
    }
}());


```