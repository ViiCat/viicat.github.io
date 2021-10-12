---
layout: post
title: "【Cocoapods】提示 -bash: pod: command not found"
date: 2018-11-16 08:00:00 +0800
categories: [iOS, Cocoapods]
---

### 报错
今天pod install时候报提示:`-bash: pod: command not found`于是按照下面的步骤一顿猛操作：

```
sudo gem install -n /usr/local/bin cocoapods
```

然后打开环境变量配置文件：

```
vim ~/.bash_profile
```
添加下面路径在文件里：

```
export GEM_HOME=$HOME/Software/ruby
export PATH=$PATH:$HOME/Software/ruby/bin
```

查看Cocoapods版本：

```
pod --version
```
结果妥妥的

<strong>参考文章</strong>
https://blog.csdn.net/zhang_15840199576/article/details/78861743