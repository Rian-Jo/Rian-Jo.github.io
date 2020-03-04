---
layout: post
title:  "[Spyder] console plot을 interactive plot으로 만들기"
subtitle:   "how to configure the interactive plot"
categories: devlog
tags: python spyder devlog
---

작업을 하고 결과 그래프를 뽑을 때 plot 툴 중 하나인 *matplotlib.pyplot* 을 사용 합니다. plot 하려고 다음의 코드를 돌리면,
![](/assets/img/docs/2020-01-30/2020-01-30-spyder-plot-code.PNG)

interaction이 가능하지 않은 plot이 Ipython console에 출력됩니다.

![](/assets/img/docs/2020-01-30/2020-01-30-spyder-inline-plot.PNG)

그래프를 움직이기도 확대해 보고 싶어도 확대가 안됩니다. 이건 IPython의 Graphic 출력(Graphic Backend)에 대한 설정이 inline으로 되어 있기 때문이다. 이 옵션은 Spyder내에서 Tools-Preference-IPython console-Graphics-Graphic Backend 라는 부분을 살펴보면 확인할 수 있습니다.

![](/assets/img/docs/2020-01-30/2020-01-30-spyder-graphic-setting.PNG)

설정 후에 콘솔을 재시작 하면, 

![](/assets/img/docs/2020-01-30/2020-01-30-spyder-interactive-plot.PNG)

새창으로 interactive plot이 출력 되는 것을 확인할 수 있습니다. 