### CentOS

#### 명령어
```{.javascript}
* ls [파일 리스트 보기]
  - F : 파일 유형을 나타내는 기호를 파일명 끝에 표시(디렉토리 /, 실행파일은 *, 심볼릭링크 @)
  - l : 파일에 관한 상세 정보
  - a : dot 파일(.access 등)을 포함한 모든 파일 표시
  
* cd [디렉토리 변경]
  - .. : 상위 디렉토리
  - cd : 어느곳에서든지 자기 홈디렉토리로 바로 이동 (cd~)
  - cd /webker : 현재 작업중인 디렉토리의 하위나 상위 디렉토리가 아닌 다른 디렉토리(webker)로 이동

* mv [파일이름(rename) / 위치(move)] 변경
  - mv index.htm index.html : 후자의 이름으로 파일명 변경
  - mv file ../main/new_file : 파일의 위치를 변경

* cp [파일 복사]
  - cp index.html index.old : index.old란 이름으로 복사
  - cp /home/test/*.* . : test 디렉토리내의 모든 파일을 현 디렉토리로 복사

* rm [파일 삭제]
  - rm test.html : test.html 파일 삭제
  - rm -r <디렉토리> : 디렉토리 전체를 삭제
  - rm -i a.* : a로 시작하는 모든 파일을 일일이 삭제할 것인지 확인하면서 삭제

* mkdir [디렉토리 생성]
  - mkdir dirname : dirname 디렉토리 생성

* rmdir [디렉토리 삭제]
  - rmdir dirname : dirname 디렉토리 삭제
```
