### 개발환경 구축 (VirtualBox + Vagrant 를 통한 centOS 설치)

```{.javascript}
1) VirtualBox와 Vagrant 설치
	- www.virtualbox.org/wiki/Downloads
	- www.vagrantup.com/downloads.html

2) 가상머신 추가
	- 터미널(cmd)을 열어서 가상 머신을 생성하고 싶은 폴더로 이동
	- 터미널 > vagrant init 실행
	- 생성된 Vagrnatfile을 편집기로 열어서 config.vm.box = "base" 부분을 "puphpet/centos65-x64"로 수정
	- 터미널 >  vagrant up 실행
	- 상기 내용을 vagrant init puphet/centos65-x64, vagrant up --provider virtualbox로 대체 가능
	- 
```
