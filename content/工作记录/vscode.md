---
title: "Vscode"
date: 2024-10-24
draft: false
---
# 一：设置相关 

## 1. vscode同步多电脑

(1) 页面左下角设置同步打开

(2) 选择需要同步的内容

(3) 登录github

(4) 同步

# 二：插件相关 #

## 1.ssh

(1) ssh到ubuntu，以及ubuntu需要的设置
https://blog.csdn.net/zsyyugong/article/details/134438071


## 2. Git->Windiows

https://blog.csdn.net/czjl6886/article/details/122129576

## 3. Git->Linux

(1) 安装git
```bash
sudo apt update
sudo apt install git
```
(2) 验证
```bash
git --version
```
(3) 配置github账户
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```
(4) 生成SSH密钥，如果有密钥直接复制过来就行，没有的话如下生成
```bash
ssh-keygen -t rsa -b 4096 -C "youremail@example.com"
```
(5) 查看密钥内容
```bash
cat ~/.ssh/id_rsa.pub
```
(6) github网页设置密钥
登录到 GitHub，然后进入 Settings > SSH and GPG keys 页面，点击 New SSH key。
粘贴复制的公钥，并为它取个名字，然后保存。
(7) 测试SSH链接
```bash
ssh -T git@github.com
```
如果成功，会显示类似于 Hi username! You've successfully authenticated, but GitHub does not provide shell access. 的消息。

# 三：快捷键
1. 显示右侧边栏
   ```bash 
   ctrl+alt+b
   ```
2. 显示左侧边栏
   ```bash
   ctrl+b
   ```
3. 显示底部边栏
   ```bash
   ctrl+j
   ```
