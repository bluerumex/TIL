### HTTP 3. Web Server

```
HTTP 메시지는 HTTP 애플리케이션 간에 주고 받는 데이터의 블록들이다.
블록들은 메시지의 내용과 의미를 설명하는 텍스트 메타 정보로 시작하고 그 다음에 선택적 데이터가 올 수 있다.

메시지는 시작줄, 헤더블록, 본문 세 부분으로 이루어짐.
시작줄 - 어떤 메시지인지 서술
헤더블록 - 속성
본문 - 데이터를 담고 있다. 본문은 아예 없을 수도 있다.

메서드의 종류
 * GET - 서버에서 어떤 문서를 가져온다 
 * HEAD - 서버에서 어떤 문서에 대해 헤더만 가져온다
 * POST - 서버가 처리해야 할 데이터를 보낸다
 * PUT - 서버에 요청 메시지의 본문을 저장한다
 * TRACE - 메시지가 프락시를 거쳐 서버에 도달하는 과정을 추적한다
 * OPTION - 서버가 어떤 메서드를 수행 할 수 있는지 확인한다
 * DELETE - 서버에서 문서를 제거한다

상태 코드
 * [전체]100 - 199 [정의된 범위] 100 - 101 [분류] 정보
 * [전체]200 - 299 [정의된 범위] 200 - 206 [분류] 성공
 * [전체]300 - 399 [정의된 범위] 300 - 305 [분류] 리다이렉션
 * [전체]400 - 499 [정의된 범위] 400 - 415 [분류] 클라이언트 에러
 * [전체]500 - 599 [정의된 범위] 500 - 505 [분류] 서버에러


```
