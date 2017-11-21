---
layout: post
title:  "如何擁有自己的 GitHub 網站"
date:   2014-12-09 10:21:00 +0800
categories: Github
---

# 步驟
1. 建立容器
    - 取得**GitHub**帳號
    - 建立**repository**，命名規則 username.github.io
2. 複製容器
```sh
git clone https://github.com/username/username.github.io
```
3. 世界您好
```sh
cd username.github.io
echo "Hello World" > index.html
```
4. 上傳
```sh
git add --all
git commit -m "Initial commit"
git push
```
**記得輸入帳號密碼**

# 參考
* [GiHub Pages][1]
[1]:https://pages.github.com/
