---
layout: post
title:  "[Python] 데이터 시각화하기 - 그래프 그리는 함수 만들기"
subtitle:   "data visualization - creating custom graph funtion"
categories: devlog
tags: python spyder devlog
---


plot 툴 중 하나인 *matplotlib.pyplot* 을 사용 합니다. 

데이터를 plotting만 하고, ppt나 다른 툴을 이용해서 덧붙여도 되지만, 이쁘게 한번에 작성하고 싶은 마음에 이것 저것 추가를 하게 됩니다.

보통 코드를 하나의 함수처럼 만들어두면 새로운 데이터나, 비슷한 다른 그래프를 그릴 때 손이 덜 가서 편합니다.

그래서 저는 *graph.py* 와 *graph_data.py* 두개의 python 파일을 만듭니다.

*graph.py*에서는 그래프 그려주는 여러개의 파일들을 한군데에 모아 관리하고, 실제 그래프는 *graph_data.py*에서 그려줍니다.

그래프를 여러개 그리는데 세팅을 매 그래프마다 그려놨다가 수정하려면 매우 귀찮기 때문에, 관련 옵션들을 한번에 변경할 수 있게 옵션을 *napedtuple*을 이용해 *graph* 함수의 인자로 넘겨주어 각각의 그래프에 적용될 수 있게 되어 있습니다.

매트랩에서 figure 그릴때마다 글자가 안이뻐서 늘 불만이었는데, figure 안에 latex 글자와 수식을 넣을 수 있어 너무 좋습니다. 


자세한 내용은 예제를 참고로..

제가 사용하는 간단한 예제입니다. 

~~~ 
# graph.py

import numpy as np
import sys
from collections import namedtuple

#####################################
# drawing function import
####################################
import graph_data

#####################################
# setting for the graph option
####################################
time = graph_data.np.genfromtxt('data.txt', encoding='ascii')[:,0];

fontsize = 11
linewidth = 0.5
title_flag = 1
error_flag = 0
each_axis_flag = 1
three_axis_flag = 0
    
start_time = 4200;
end_time = len(time);



graphOption = namedtuple('graphOption', ['fontsize', 'linewidth', 'title_flag', 'error_flag', 'each_axis_flag', 'three_axis_flag', 'start_time', 'end_time'])

graph_option = graphOption(fontsize, linewidth, title_flag, error_flag, each_axis_flag, three_axis_flag, start_time, end_time)


#####################################
# list of graphs
# if it is necessary to adjust the time range,
# add start_time and end_time in the drawing function
# graph_data.Graph(graph_option);
####################################
graph_data.Graph(graph_option);

~~~


~~~ 
# graph_data.py

import numpy as np
import matplotlib.pyplot as plt

def Graph(graph_options):
    
    fontsize = graph_options.fontsize
    _linewidth = graph_options.linewidth
    title_flag = graph_options.title_flag
    flag_error = graph_options.error_flag
    start_time = graph_options.start_time;
    end_time = graph_options.end_time;

    
    #####################################
    # data parsing
    ####################################
    FILE_data = np.genfromtxt('data.txt', encoding='ascii')
    
    
    # time data parsing
    time = FILE_data[:,0:1];
    
    if end_time == None:
        end_time = len(time);
    
    # force data parsing
    data = FILE_data[:,1:7];
    
    
    
    #####################################################################
    # setting figures
    #####################################################################
    
    # use LaTeX fonts in the plot
    plt.rc('text', usetex=True)
    plt.rc('font', family='serif')
    
    
    #####################################################################
    # plot the figure
    #####################################################################
    # set figure
    Fig = plt.figure()
    
    # plot body position
    plt.plot(time[start_time:end_time], data[start_time:end_time,0:3], '--', linewidth=_linewidth)
    plt.plot(time[start_time:end_time], data[start_time:end_time,3:6], '-', linewidth=_linewidth)
    # set labels (LaTeX can be used)
    if title_flag == 1:
        plt.title(r'\textbf{force}', fontsize=fontsize)
    
    plt.xlabel(r'\textbf{time (s)}', fontsize=fontsize)
    plt.ylabel(r'\textbf{linear force (N)}', fontsize=fontsize)
    plt.legend(['$x_d$', '$y_d$', '$z_d$','x', 'y', 'z'], frameon=False)
    plt.show()
    
    Fig.savefig("./figures/eps/data.eps", bbox_inches='tight')
    Fig.savefig("./figures/png/data.png", bbox_inches='tight')  

~~~

