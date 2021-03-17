---
layout: post
title:  "[System] Pinocchio 설치 및 실행"
subtitle:   "WSL, Ubuntu 20.04 LTS, C++, robot package, pinocchio"
categories: devlog
tags: system devlog
---

휴머노이드 로봇을 연구하는 그룹 중 핫한 그룹인 CNRS에서 개발한 [*Pinocchio*](https://stack-of-tasks.github.io/pinocchio/) 라는 로봇 패키지를 사용해보고자 합니다. 위 패키지는 리눅스 기반 패키지 이기에 [윈도우 10 환경에서 WSL(Windows Subsystem for Linux)를 이용해 우분투 20.04 LTS 사용 환경을 만들어]() 설치를 진행 합니다. 

---
## [pinocchio 및 robotpkg 설치](https://stack-of-tasks.github.io/pinocchio/download.html)

### robotpkg 설치
*pinocchio*는 *robotpkg*를 기반으로 하기에, [*robotpkg*](http://robotpkg.openrobots.org/install.html)를 먼저 설치해야 합니다. 경로가 중요하므로, 메뉴얼과 사용자의 경로를 잘 구분해 설치를 진행해야 합니다.

우분투를 실행하면 필자의 경우 ./home/jhjo 경로에서 시작이 됩니다. 여기에서 작업경로를 ./opt 로 바꾸고, openrobots 폴더를 만든 후 아래 깃 명령어를 통해 robotpkg를 깃허브 사이트에서 다운로드 합니다.

```
cd .. # ./home 경로로 이동
cd .. # ./ 경로로 이동
cd opt/ # ./opt 경로로 이동
sudo mkdir openrobots # openrobots란 이름의 폴더 생성
git clone git://git.openrobots.org/robots/robotpkg # robotpkg 다운로드
```

![](/assets/img/docs/2021-03/2021-03-18-robotpkg-install.JPG)


* 현재 폴더 열기를 통해 현재 작업중인 경로 확인 가능
```
explorer.exe .
```

### Bootstrap
*robotpkg*를 사용하려면 꼭 [*bootstrap*](http://robotpkg.openrobots.org/install.html)이 필요하다. c compiler가 꼭 필요하고, 경로를 잘 확인하여 작업을 해두어야 한다. 사용자 경로를 기본경로와 다르게 할 경우, --prefix 를 이용해 경로를 잡아주고 환경변수 설정이 필요하다. 필자의 경우 기본경로에 설정을 하였으므로, 다음의 명령을 통해 bootstrapping이 가능하다.
```
cd robotpkg/bootstrap 
./bootstrap
```

![](/assets/img/docs/2021-03/2021-03-18-bootstrap-install.JPG)

---
### robotpkg 업데이트
Bootstrapping 이후에 robotpkg를 업데이트 해주어야 한다.

```
cd ..
sudo make update confirm
```


### pinocchio 설치
*pinocchio* 설치과정으로 사이트에 나와있는 과정을 그대로 따라해주면 된다.
```
 sudo apt install -qqy lsb-release gnupg2 curl

 echo "deb [arch=amd64] http://robotpkg.openrobots.org/packages/debian/pub $(lsb_release -cs) robotpkg" | sudo tee /etc/apt/sources.list.d/robotpkg.list

 curl http://robotpkg.openrobots.org/packages/debian/robotpkg.key | sudo apt-key add -

 sudo apt-get update

 sudo apt install -qqy robotpkg-py38-pinocchio
```
웹사이트에는 마지막줄의 파이썬버전을 py27로 되어 있는데 필자의 시스템은 파이썬버전을 3.8을 사용하고 있어 py38로 바꾸어 설치하였다.

마지막으로 환경변수를 설정해주면 끝이다. 필자는 아래의 코드를 $home/jhjo/.bashrc 의 파일 마지막 부분에 추가해주었다.

```
export PATH=/opt/openrobots/bin:$PATH
export PKG_CONFIG_PATH=/opt/openrobots/lib/pkgconfig:$PKG_CONFIG_PATH
export LD_LIBRARY_PATH=/opt/openrobots/lib:$LD_LIBRARY_PATH
export PYTHONPATH=/opt/openrobots/lib/python2.7/site-packages:$PYTHONPATH # Adapt your desired python version here
export CMAKE_PREFIX_PATH=/opt/openrobots:$CMAKE_PREFIX_PATH
```

했는데 안됨....ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ


