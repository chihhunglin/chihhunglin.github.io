---
layout: post
title:  "使用 Packer 建立 Windows VM box"
date:   2016-05-06 17:30:00 +0800
categories: DevOps
---

  學習 [Packer][1] 筆記．(不完整版)

## 安裝
參閱官方[文件][2]

## 實作 Windows
[Setup a local Windows 2016 TP5 Docker VM][3]

## Run Packer

* Packer version : 0.10.0
* Virtualbox version : 5.0.20
* Vagrant : 1.8.1

```sh
git clone https://github.com/StefanScherer/packer-windows
cd packer-windows

packer build --only=virtualbox-iso windows_2016_docker.json
```

* [key][4]

# 參考
* [Using Packer to package Vagrant box(driver: Virtualbox) by Docker][5]


[1]:https://www.packer.io/
[2]:https://www.packer.io/docs/installation.html
[3]:https://stefanscherer.github.io/setup-local-windows-2016-tp5-docker-vm/
[4]:https://blogs.technet.microsoft.com/ausoemteam/2016/04/28/windows-server-2016-technical-preview-5-available-for-download/
[5]:https://github.com/seterrychen/packer-vagrant-vbox
