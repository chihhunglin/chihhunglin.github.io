---
layout: post
title:  "install dlib on mac"
date:   2018-01-01 16:03:06 +0800
categories: python dlib
---
環境:
{% highlight shell %}
Mac: macOS High Sierra Version 10.13.2
Homebrew: 1.4.2
pyenv: 1.1.5
gcc: Apple LLVM version 9.0.0 (clang-900.0.39.2)
Boost: 1.66.0
{% endhighlight %}

Step:
{% highlight shell %}
$ brew install boost
$ pyenv global 3.5.4 2.7.14
$ pyenv rehash
$ pyenv versions
system
* 2.7.14 (set by /Users/peter/.pyenv/version)
* 3.5.4 (set by /Users/peter/.pyenv/version)
$ brew install boost-python --with-python3
$ pyenv activate venv
$ pip install dlib
{% endhighlight %}

如果缺少shared lib
請再次安裝python
{% highlight shell %}
PYTHON_CONFIGURE_OPTS="--with-dtrace --enable-shared" pyenv install 3.5.4
{% endhighlight %}
