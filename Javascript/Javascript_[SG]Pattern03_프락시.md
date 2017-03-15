### JavaScript 프락시 패턴

#### 프락시 패턴
```{.javascript}
프락시 패턴은 말 그대로 하나의 객체가 프락시 역할을 수행하여 상황에 따라 다른 객체에 접근하게 해주거나
다른 함수를 호출하게 해주는 패턴이다.

프락시는 클라이언트와 서버 사이에서 중간자 역할을 한다.
프락시의 역할 중 대표적인 것은 클라이언트가 서버에 직접 접근하지 못하도록, 한 단계 가상화 또는
캡슐화하는 기능이다.

또한, 클라이언트가 request를 프락시에 한 번만 전달하면, 프락시는 서버로 여러번의 복잡한 real request를 보낸다.
응답 또한 마찬가지로 서버가 여러 개의 real response를 보내면 프락시에 취합하여 하나의 response로 
보내는 기능을 수행한다. 부가적으로 웹에서의 프락시는 캐시 기능을 수행하기도 한다.

패턴 예제)

proxyClickEventHandler = {
    "play": function() {
        videoBunny.play();
    },
    "pause": function () {
        videoBunny.pause();
    },
    "volumeUp": function () {
        if (videoBunny.volume <= 0.9) {
            videoBunny.volume += 0.1;
        } else {
            videoBunny.volume = 1;
        }
    },
    "volumeDown": function () {
        if (videoBunny.volume >= 0.1) {
            videoBunny.volume -= 0.1;
        } else {
            videoBunny.volume = 0;
        }
    }
};

divControlPanel.addEventListener("click", function (e) {
   var target = e.target || e.srcElement; //e.srcElemnet IE8 Under
    if (proxyClickEventHandler.hasOwnProperty(target.id)) {
        proxyClickEventHandler[target.id].call();
    }
}, true);

또한 캐쉬 기능을 프락시 패턴과 조합해서 사용하면 XMLHttpRequest를 보낼 때도 주기적으로 변경되지
않는 동일한 응답이 필요할 때 서버와의 통신을 최소화 할 수 있다.

<body>
<video style="width:240px" id="videoBunnySmall" src="http://media.w3.org/2010/05/bunny/movie.ogv"></video>
<video style="width:320px" id="videoBunnyMedium" src="http://media.w3.org/2010/05/bunny/movie.ogv"></video>
<video style="width:480px" id="videoBunnyLarge" src="http://media.w3.org/2010/05/bunny/movie.ogv"></video>

<div id="controlPanel">
    <select id="controlVideo">
        <option>videoBunnySmall</option>
        <option>videoBunnyMedium</option>
        <option>videoBunnyLarge</option>
    </select>
    <button id="play">Play</button>
    <button id="pause">Pause</button>
    <button id="volumeUp">Volume+</button>
    <button id="volumeDown">Volume-</button>
</div>

<script>
    (function () {
        var divControlPanel = document.getElementById("controlPanel"),
            selectControlVideo = document.getElementById("controlVideo"),
            controlVideo = {
                "play": function(video) {
                    video.play();
                },
                    "pause": function (video) {
                        video.pause();
                },
                "volumeUp": function (video) {
                    if (video.volume <= 0.9) {
                        video.volume += 0.1;
                    } else {
                        video.volume = 1;
                    }
                },
                "volumeDown": function (video) {
                    if (video.volume >= 0.1) {
                        video.volume -= 0.1;
                    } else {
                        video.volume = 0;
                    }
                },
                "getVideoId": function (id) {
                    return document.getElementById(id);
                }
            },
            proxyClickEventHandler = (function() {
                var cache = {};
                return function (command) {
                  var video;
                    if (controlVideo.hasOwnProperty(command)) {
                        if (cache.hasOwnProperty(selectControlVideo.value)) {
                            video = cache[selectControlVideo.value];
                        } else {
                            video = controlVideo.getVideoId(selectControlVideo.value);
                            cache[selectControlVideo.value] = video;
                        }
                        controlVideo[command].call(this, video);
                    }
                };
            }());


        divControlPanel.addEventListener("click", function (e) {
            var target = e.target || e.srcElement; //e.srcElemnet IE8 Under
            proxyClickEventHandler(target.id);
        }, true);
    }());
</script>
</body>
```