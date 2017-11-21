---
layout: post
title:  "Vagrant + Ansible"
date:   2015-01-27 17:30:00 +0800
categories: DevOps
---

# Vagrant
## [虛擬機][1]
```cmd
mkdir demo-1
cd demo-1
vagrant init ubuntu/trusty64
vagrant up
```
## 登入Ubuntu
```cmd
vagrant ssh
```

## 登出
```cmd
vagrant$  exit
```

## 關機
```cmd
vagrant halt
```

# Ansible
## 安裝[Ansible][3]
```sh
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

## 配置[authorized_keys][4]
### 產生key
```sh
$ ssh-keygen -t rsa
```
### 配置遠端public key
```sh
$ cat ~/.ssh/id_rsa.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## [基礎用法][5]
### 編輯inventory file
>hosts

```
[test]
127.0.0.1
```

### ping module
```sh
$ ansible -m ping -i hosts -u vagrant test
```

## [利用 Ansible 部署 GitHub 專案的設定細節][2]
### clone 範例
```sh
$ git clone https://github.com/William-Yeh/ansible-git-deploy-demo.git
```

### 下載 roles
```sh
$ cd ansible-git-deploy-demo/public-repo
$ ansible-galaxy install -f  -r requirements.yml
```

### 執行劇本
#### 編輯hosts
```sh
$ ansible-playbook -i hosts -u vagrant playbook.yml
```

### 確認安裝成功
```sh
wrk --help
```

[1]:http://www.codedata.com.tw/social-coding/vagrant-tutorial-2-playing-vm-with-vagrant/
[2]:http://www.codedata.com.tw/social-coding/ansible-github/
[3]:http://docs.ansible.com/intro_installation.html#latest-releases-via-apt-ubuntu
[4]:http://askubuntu.com/questions/46424/adding-ssh-keys-to-authorized-keys
[5]:http://www.lemonlatte.tw/tags/Ansible
