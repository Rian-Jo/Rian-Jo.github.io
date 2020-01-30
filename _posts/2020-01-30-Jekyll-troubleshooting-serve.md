---
layout: post
title:  "Jekyll error - Invalid CP949 character '\ xE2'"
subtitle:   "character encoding error"
categories: devlog
tags: jekyll blog theme devlog
---

기본 지킬 작업 환경을 만든 후에, 
```
jekyll serve
```
명령으로 local host에서 블로그 페이지가 잘 보였습니다.

하지만 테마를 입힌 후에 다시 시도를 하니 여러가지 문제가 발생합니다.

기본적으로 위의 명령어가 동작을 안해서
```
bundle exec jekyll serve
```
명령어로 실행을 시키면 잘 동작한다.

---

두번째 문제로, 

UTF-8 encoding을 사용하기에 나타나는 에러이다.

![](/assets/img/docs/2020-01-30/2020-01-30-invalid-character.PNG)

콘솔 창에서 다음과 같이 입력한 후, 
```
chcp 65001
```
지킬을 실행시키면 잘 된다.

