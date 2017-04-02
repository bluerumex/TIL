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
