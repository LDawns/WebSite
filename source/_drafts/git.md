---
title: 万能的git使用教程
tags: 
- git
categories: 
- git
date: 2019-07-07
---

# 测试git环境---创建第一个README.md

- 新建一个目录test
```
mkdir test
cd test
```
- 然后将其作为git文件夹
```
git init
```

如果成功，将会生成一个.git隐藏目录

- 在文件夹中做一些修改
```
vim README.md
```
在`READEME.MD`中随便加入一些文字内容

- 将该文件夹下所有文件加入git追踪
```
git add .
```
git默认文件处于不跟踪状态，每一个文件都不外乎这两种状态：已跟踪或未跟踪。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区（暂存区是提交之前的一个临时区域）。 工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有放入暂存区。这样的处理让你不必担心将生成的二进制文件或其它不想被跟踪的文件包含进来。

- 把项目提交到缓冲区中
```
git commit -m 'tets commot'
```
到这里我们就需要与网页上的github进行联动了，既然要联动，就必须要有一个验证机制

- 生成密钥
```
ssh-keygen -C 'email' -t rsa
```
一路默认即可，过程中会提示在某某某目录下创建了两个密钥，一个为私钥，一个为公钥，私公钥加密体系这里不再提及，总之我们需要的是公钥`id_rsa.pub`，复制其内容(可以包含最后的邮箱也可以不包含，但最前面的rsa必须包含)

打开网页版的github，登入你的账号，找到设置`setting`选项，点击`SSH and GPG keys`,点击`New SSH Keys`页面，填上你想要的标题，粘贴你的公钥，点击`Add Key`即可

- 添加远程仓库
```
git remote add origin git@github.com:your_userid/your_repository_name
```

- 推送缓冲区内容
```
git push origin master
```
在这里你可能会遇到一些问题，比如403 forbidden,这里提供一些解决方案：
1. 检查并设置全局用户名与密码
```
git config  --global user.name your_userid
git config  --global user.email your_email
git config --global user.password your_password
```
2. 更改.git文件夹的内容
```
vim .git/config
```
将url是改成如下摸样：
```
url = https://用户名:密码@github.com/sdoyuxuan/K-V-.git
```


未完待续...
 
