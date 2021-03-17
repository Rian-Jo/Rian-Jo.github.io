---
layout: post
title:  "[System] 윈도우 10에서 WSL로 우분투 개발환경 설정"
subtitle:   "Ubuntu 20.04 LTS, C++"
categories: devlog
tags: system devlog
---

윈도우 10 환경에서 WSL(Windows Subsystem for Linux)를 이용해 우분투 20.04 LTS 사용 환경을 만들어보고자 합니다.  

---
### WSL 설치
[WSL_install] 에 따라 cmd 실행 후 *wsl --install* 명령어 입력으로 간단히 설치 가능합니다.

---
### Ubuntu 20.04 LTS 설치
WSL 설치 후에 재부팅을 하고 나면, 마이크로소프트 스토어에서 우분투를 간단히 다운로드 및 설치가 가능합니다. 여러개가 나오는데, 아래 사진의 두번째 앱은 다운로드가 잘되지 않습니다. 첫번째 앱의 설명에 ubuntu 20.04 LTS 버전이라는 설명이 있으므로 첫번째 앱을 다운로드 및 설치 하면 됩니다.

![](/assets/img/docs/2021-03/2021-03-17-MSStore-ubuntu.JPG)

---
### Ubuntu 20.04 LTS 에서 컴파일러 설치

```
# sudo apt-get install build-essential
```






[WSL_install]: https://docs.microsoft.com/en-us/windows/wsl/install-win10
