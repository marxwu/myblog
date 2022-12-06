---
title: "Hugo创建博客"
date: 2022-12-05T23:34:11+08:00
draft: false

featured_image: "images/hugo-github.png"
tags: ["hugo", "github", "markdown", "git"]
categories: "hugo"
---

mac下实践

# hugo create blog

1. 安装hugo
``` hugo install on macbook
myblogprj % brew install hugo
myblogprj % hugo version
myblogprj % brew reinstall hugo
```

2. 建立博客根目录myblog，添加theme，运行起来
```
myblogprj % hugo new site myblog

myblogprj % cd myblog

myblog % mkdir themes
myblog % git clone https://github.com/AmazingRise/hugo-theme-diary.git --depth=1 themes/diary
myblog % cp -r themes/diary/exampleSite/content ./
myblog % cp themes/diary/exampleSite/config.toml ./

myblog % hugo server
```
&emsp;&emsp;访问http://localhost:1313/

3. 建立第一个博客，然后用vscode编辑内容

```
myblog % hugo new posts/数学高一知识点.md
```

&emsp;&emsp;用vscode编辑：
```
---
title: "数学高一知识点"
date: 2022-12-06T21:47:46+08:00
draft: false

featured_image: "images/emc2.png"
tags: ["数学", "高一"]
categories: "高中数学"
---

# 集合
# 不等式
# 指数和对数
# 函数
## 幂函数
## 指数函数

```


# git and github

1. 设置github可以用ssh方式连接

```
git安装比较大众化，安装完之后设置你的github用户名和email
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
$ git config --list

使用默认值生成密钥对：
% ssh-keygen -t rsa -C "yourmail@qq.com"
MacBook-Pro ~ % cd .ssh
MacBook-Pro .ssh % ls
id_boot2docker		id_boot2docker.pub	id_rsa			id_rsa.pub		known_hosts

公钥id_rsa.pub的文本内容copy到github
Settings -> SSH and GPG keys 设置

测试github是否能连上：
myblog % ssh -T -p 443 git@ssh.github.com
Hi soyawu! You've successfully authenticated, but GitHub does not provide shell access.


```

```
如果突然出现这个问题：
myblog % git push -u origin master
ssh: connect to host github.com port 22: Operation timed out
fatal: Could not read from remote repository.

% vim ~/.ssh/config
Host github.com
 Hostname ssh.github.com
 Port 443

ssh -T git@github.com
```

```
命令行终端设置代理：
export http_proxy=http://192.168.1.101:8888
export https_proxy=http://192.168.1.101:8888

git设置代理：
git config --global http.proxy http://192.168.1.101:8888
```

# deploy blog on github
这个仓库用于blog的源代码：  
https://github.com/yourname/myblog.git
git@github.com:yourname/myblog.git

这个仓库用来发布blog，即hugo生成的public目录的站点内容：  
https://github.com/yourname/myblogpublic.git
git@github.com:yourname/myblogpublic.git

```
myblog % git remote -v
myblog % git remote add origin https://github.com/marxwu/myblog.git

myblog % git add . 
myblog % git commit -m "committing my hugo blog src" 
myblog % git push -u origin master
```

```
submodule貌似不好用：
git submodule add -b master <repo.git> <folder>
myblog % git submodule add -b master git@github.com:marxwu/myblogpublic.git public
以上添加子模块public都不成功。只能先用.gitignore忽略。

用户hugo命令生成public文件：
myblog % hugo
public % git init
public % git remote add origin git@github.com:marxwu/myblogpublic.git
public % git status
public % git add .
public % git commit -m 'pubic first version'

myblog % git push -u origin master
```


最后在myblogpublic仓的Settings->Pages中
设置https://yourname.github.io/myblogpublic/仓，发布站点。

  

注意config.toml中编辑：
```
baseURL = "https://yourname.github.io/myblogpublic"
DefaultContentLanguage = "zh" # Theme's display language, supports: en, fr, zh, zh-hant
languageCode = "zh-CN"
title = "千山暮雪"
copyright = "202X yourname"
theme = "diary"
```

你就可以访问博客了：https://yourname.github.io/myblogpublic


# references
