### 개발환경 구축 (VirtualBox + Vagrant 를 통한 centOS 설치)

```{.javascript}
1) VirtualBox와 Vagrant 설치
  - www.virtualbox.org/wiki/Downloads
  - www.vagrantup.com/downloads.html
  - vagrant란 가상 머신을 편리하게 사용할 수 있도록 도와주는 툴

2) 가상 머신 추가
  - 터미널(cmd)을 열어서 가상 머신을 생성하고 싶은 폴더로 이동
  - 터미널 > vagrant init 실행
  - 생성된 Vagrnatfile을 편집기로 열어서 config.vm.box = "base" 부분을 "puphpet/centos65-x64"로 수정
  - 터미널 >  vagrant up 실행
  - 상기 내용을 vagrant init puphet/centos65-x64, vagrant up --provider virtualbox로 대체 가능

3) 가상 머신 제어
  - vagrant up : 실행
  - vagrant status : 가상 머신의 기동 상태를 확인하기 위한 명령어 
  - vagrant halt : 정지
  - vagrant suspend : 휴면
  - vagrant resume : 휴면 상태에서 복원
  - vagrant reload : 재기동
  - vagrant destroy : 가상 머신 삭제
  - vagrant ssh : 가상 머신에 로그인

4) 가상 머신에 로그인
  - vagrant ssh 명령으로 SSH 접속에 필요한 정보를 얻어온다
  - Poderosa를 실행해 해당 정보를 입력
```
#### node 명령어
```{.javascript}
1) 모듈 설치
 - npm install (모듈이름)
   모듈을 설치학 되면 그 모듈에서 의존하는 모듈도 자동으로 같이 설치 된다

2) 모듈이 설치되는 경로
 - 기본적으로 npm install로 설치하면 이 명령을 실행한 현재 디렉토리에 모듈이 다운된다 
   현재 디렉토리에 node_module라는 디렉토리가 만들어지고, 그 안에 모듈이 다운된다
   
3) 글로벌 설치 -g
 - npm instal -g (모듈이름)
   글로벌 설치할 때 주의점은 대부분의 환경에서 관리자의 권한이 필요하다는 점이다
   CentOS나 Mac OS X에서는 명령어 앞에 sudo를 붙여서 관리자 권한으로 명령을 실행
   
   sudo npm install -g (모듈이름)
   
4) 글로벌 설치 시 path 주의
 - npm root -g // 글로벌 설치 경로 확인
 - Error: Cannot find module '(모듈이름)'
   모듈을 아직 설치 하지 않았거나 Node.js 에서 npm으로 글로벌하게 설치한 모듈을 찾을 수 없을때 발생
   
5) 모듈을 찾을 때 검색하는 경로
 - node -e "console.og(global.module.paths)"
   현재 작업 디렉토리의 node_module 폴더, 그리고 상위 폴더의 node_module 폴더,
   그리고 그 상위 폴더의 node_module폴더.. 이런 순으로 차례대로 모듈을 검색
   이와 별개로 node.js는 환경 변수 NODE_PATH에 저장된 경로도 검색한다.
```
