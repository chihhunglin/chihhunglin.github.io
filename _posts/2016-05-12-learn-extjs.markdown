---
layout: post
title:  "測試 Extjs"
date:   2016-05-12 14:30:00 +0800
categories: frontend
---

  學習 [Ext JS][1] 筆記．

## 安裝
參閱官方[文件][2]

* 下載試用版 : Download and Install Sencha Cmd 6
* 下載SDK : Download and unzip the Ext JS SDK

## 使用 Sencha Cmd 建立 Ext JS 6 應用程式
* 打開console window (小魯的是 Win10)
* [操作手冊][3]

```sh
sencha -sdk /path/to/ext6 generate app MyApp /path/to/my-app
```

### 進行開發

```sh
cd /path/to/my-app
sencha app watch
```

### 瀏覽

> http://localhost:1841/

![Imgur](http://i.imgur.com/VEUK0K7.png?1)

## 建構一個登入系統
[範例][4]

![Imgur](http://i.imgur.com/BcVGxk8.png?1)

![Imgur](http://i.imgur.com/8Crue8E.png?1)

[1]:https://www.sencha.com/
[2]:http://docs.sencha.com/extjs/6.0/getting_started/welcome_to_extjs.html
[3]:https://docs.sencha.com/cmd/6.x/extjs/cmd_app.html
[4]:https://docs.sencha.com/extjs/6.0/getting_started/login_app.html#Step_1___Generate_your_Application
