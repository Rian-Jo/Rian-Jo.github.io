---
layout: post
title:  "Jekyll error - The 'gems' configuration option has been renamed to 'plugins'"
subtitle:   "Please update your config file accordingly."
categories: devlog
tags: jekyll blog theme devlog
---


테마 설정 후에,  
```
bundle exec jekyll serve
```
명령어로 실행을 시켰을 때 다음과 같이 Deprecation 메시지가 보이면,

![](/assets/img/docs/2020-01-30/2020-01-30-gems-to-plugins.PNG)

config.yml 파일에서 "gems:" 를 찾은 후, "plugins:"로 바꿔주면 된다.


