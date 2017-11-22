---
layout: post
title:  "darkflow in macOS"
date:   2017-11-22 16:03:06 +0800
categories: tensorflow darknet deep-learning object-detection machine-learning
---
[YOLO: Real-Time Object Detection][yolo]
目標是想要可以在macOS上用camera跑demo(沒有nvidia
GPU)，於是找到[darkflow][darkflow]，記錄實作過程如下：

環境需求：Python3, tensorflow 1.0, numpy, opencv 3.

Python使用pyenv安裝，用3.6.x會失敗．
virtualenv用pyenv virtualenv．
{% highlight shell %}
pyenv install 3.5.4
pyenv shell 3.5.4
pyenv virtualenv venv
pyenv activate venv
{% endhighlight %}

{% highlight shell %}
pip install Cython
pip install numpy
pip install opencv-python
pip install --upgrade tensorflow
pip list
>>
Cython (0.27.3)
numpy (1.13.3)
opencv-python (3.3.0.10)
tensorflow (1.4.0)
{% endhighlight %}

之後的安裝步驟照著darkflow readme，[getting-started][getting-started]

{% highlight shell %}
git clone https://github.com/thtrieu/darkflow.git
cd darkflow
pip install -e .
{% endhighlight %}

{% highlight shell %}
flow --h
>>
Example usage: flow --imgdir sample_img/ --model cfg/yolo.cfg --load bin/yolo.weights
{% endhighlight %}

下載weights，從yolo
{% highlight shell %}
wget https://pjreddie.com/media/files/yolo.weights
mv yolo.weights bin/.
{% endhighlight %}

可以開始使用，輸出的video會放在同個目錄下。
{% highlight shell %}
flow --model cfg/yolo.cfg --load bin/yolo.weights --demo camera --saveVideo
{% endhighlight %}


[yolo]: https://pjreddie.com/darknet/yolo/
[darkflow]: https://github.com/thtrieu/darkflow
[getting-started]: https://github.com/thtrieu/darkflow#getting-started
