---
layout: post
title:  "使用 Pelican 創造自己的 Github Pages blog"
date:   2016-04-25 14:30:00 +0800
categories: Github
---

  [Pelican][2] 用 python 寫成的靜態網頁產生工具．

# 設定 github.io 網頁
* 建立兩個容器
    - 取得 **GitHub** 帳號
    - 建立 **repository** ，命名規則 username.github.io-src and username.github.io(初始化加入README)

# 安裝 Pelican
```sh
pip install pelican markdown
git clone https://github.com/username/username.github.io-src ghpages
cd ghpages
```

# 使用 Pelican 設定 Blog
```sh
git remote -v
git submodule add https://github.com/username/username.github.io output
pelican-quickstart
```
* Where do you want to create your new web site? (hit Enter)
* What will be the title of this web site? (ex:Blog)
* Who will be the author of this web site? (ex:Peter)
* What will be the default language of this web site? [en] (hit Enter)
* Do you want to specify a URL prefix? e.g., http://example.com   (Y/n) (Y)
* What is your URL prefix? (see above example; no trailing slash) (http://chihhunglin.github.io)
* Do you want to enable article pagination? (Y/n) (n)
* What is your time zone? [Europe/Paris] (Asia/Taipei)
* Do you want to generate a Fabfile/Makefile to automate generation and publishing? (Y/n) (Y)
* Do you want an auto-reload & simpleHTTP script to assist with theme and site development? (Y/n) (Y)
* Upload mechanisms: choose No for all except Github Pages
* Is this your personal page (username.github.io)? (y/N) (Y)

Open the publishconf.py file and set the DELETE_OUTPUT_DIRECTORY variable to False.

Error: [Errno 17] File exists: '/Users/hung/Github/ghpages/output' (這個錯誤不用理）

# Init, update submodule (非必要)
```sh
git submodule init
git submodule update
```

# Build, commit, push, 完成!
```sh
make html && make serve
make publish

cd output
git add .
git commit -m "First commit."
git push -u origin master
cd ..
echo '*.pyc' >> .gitignore #don't need pyc files
git add .
git commit -m "First commit."
git push -u origin master
```

# 參考

* [GiHub Pages][1]
* [Make a Github Pages blog with Pelican][3]
[1]:https://pages.github.com/
[2]:http://docs.getpelican.com/en/3.6.3/
[3]:https://fedoramagazine.org/make-github-pages-blog-with-pelican/
