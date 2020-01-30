---
layout: post
title:  "Jekyll - 배경색 바꾸기"
subtitle:   "background color change"
categories: devlog
tags: jekyll blog theme devlog
---

개인적으로 하얀색 배경 페이지를 꺼려한다. 오래보고 있으면 눈이 아파서, 윈도우 배경, vs 등의 개발환경, 크롬 등등 다크 테마로 바꾸어 쓸 수 있는 것들은 죄다 바꾸어 사용하는 편이다. 현재 사용 중인 Hyde 테마의 경우, 기본이 하얀 배경이고, pro 버전으로 유료 업그레이드를 하면 다크모드도 사용할 수 있다고 한다. 하지만 유료 버전까지는 필요 없을 듯 하여, 직접 배경색을 바꾸어 보고자 한다.

---

기본적으로 페이지의 형태를 설정하는 부분은 sass 폴더의 각 요소들에 들어가 있다. 
![](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-tree.PNG)

우리는 페이지 전체 배경의 색을 바꿔줄 것이기 때문에, `base-inline.scss` 에 들어가 배경 요소를 추가한다.

![](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-bg-add.PNG)

후에, 빌드하여 실행하면 다음과 같은 변화를 확인할 수 있다.

![배경색 추가 전](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-bg-before-change.PNG)


![배경색 추가 후](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-bg-after-change.PNG)

배경색이 바뀌면서 글자가 하나도 보이지 않는다. 분명 폰트는 검은색이었을텐데... 

그리하여 같은 폴더에 `_content-inline.scss` 파일을 보면 컨텐츠의 설정에 해당하는 요소들이 보이고, 여기에 다음과 같이 폰트의 색을 설정한다.

![](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-font-color-add.PNG)

다음과 같이 폰트색이 바뀐 것을 확인할 수 있다.

![폰트색 추가 후](/assets/img/docs/2020-01-30/2020-01-30-jekyll-ssas-font-color-after-change.PNG)


---

