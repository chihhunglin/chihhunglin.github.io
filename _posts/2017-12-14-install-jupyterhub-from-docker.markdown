---
layout: post
title:  "install jupyterhub from docker"
date:   2017-12-24 16:03:06 +0800
categories: tensorflow python jupyter jupyterhub
---
Run:
{% highlight shell %}
docker run -p 8000:8000 -d --name jupyterhub jupyterhub/jupyterhub:0.8.1
jupyterhub
{% endhighlight %}

Go to container[jupyterhub]:
{% highlight shell %}
docker exec -it jupyterhub bash
{% endhighlight %}

Setting:
{% highlight shell %}
useradd -m -p /home/admin admin
passwd admin
pip install notebook
{% endhighlight %}
