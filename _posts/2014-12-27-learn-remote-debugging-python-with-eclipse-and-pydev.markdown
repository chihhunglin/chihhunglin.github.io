---
layout: post
title:  "Remote Debugging Python with Eclipse and PyDev"
date:   2014-12-27 14:30:00 +0800
categories: Python
---

原文請參閱[Blog][1]，本文新增自己的實作過程。
環境介紹
> Local : Win8 + eclipse + PyDev

> Remote : ubuntu + python2.7 in virtualbox

1. 安裝[eclipse][2]
請先安裝[Java][3]，我安裝的是Java 8 跟 eclipse jee luna。

2. 安裝[PyDev][4]

3. 建立PyDev專案，設定python interpreter(注意要跟遠端執行的同一個minor版本)
    - 安裝[python interpreter][5]
    - 在Eclipse 設定 python interpreter，參考 [2.3.1 Add Python Interpreter Path ][6]
    - 建立專案

        > File -> New -> PyDev Project
      > [PyDev Project]dialog
      > Project name: 自己打一個
      > Project contents: 程式放置目錄
      > Interpreter: 選剛才設定Python27
      > Finish

4. 複製pydev到遠端機器
```sh
find /Applications/eclipse/plugins -name 'org.python.pydev_*'
```
e.g. /Applications/eclipse/plugins/org.python.pydev_2.8.2.2013090511

        將檔案放置到正確路徑
```sh
python -c "import sys
from pprint import pprint as pp
pp(sys.path)"
```
e.g. /usr/local/lib/python2.7/dist-packages
```sh
ssh vagrant@example.dev mkdir pysrc
scp -r /Applications/eclipse/plugins/org.python.pydev_2.8.2.2013090511/pysrc/* vagrant@example.dev:pysrc
ssh vagrant@example.dev 'sudo cp -R pysrc/* /usr/local/lib/python2.7/dist-packages/'
ssh vagrant@example.dev rm -r pysrc
```

5. 設定路徑對照
在 ubuntu 編輯 /usr/local/lib/python2.7/dist-packages/pydevd_file_utils.py
```sh
PATHS_FROM_ECLIPSE_TO_PYTHON = [
        (r'C:\Gitlab\xxx\rrr', r'/home/vagrant/xxx/rrr')
]
```
**注意大小寫**

6. 新增程式
當 py 執行到 settrace 會中斷去連結到 eclipse 的 debug server。 譬如寫在 run.py。
在 ubuntu 執行 **netstat -rn** 可以知道 default gw 就是 Host(eclipse) 的IP。
```py
# append path
sys.path.append(r'/usr/local/lib/python2.7/dist-packages')
import pydevd
# breakpoint
pydevd.settrace('10.0.2.2', port=5678, stdoutToServer=True, stderrToServer=True)
```

7. 啟動 eclipse debug server
see [PyDev | Remote Debugger][1]

8. 執行python
grunt serve

#重要
兩邊的程式碼一定要一樣，斷點才會有效果。

[1]: http://brianfisher.name/content/remote-debugging-python-eclipse-and-pydev
[2]: https://eclipse.org/
[3]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[4]: http://pydev.org/manual_101_install.html
[5]: https://www.python.org/downloads/
[6]: http://kodi.wiki/view/HOW-TO:Debug_Python_Scripts_with_Eclipse
