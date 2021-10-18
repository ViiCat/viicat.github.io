---
title: 自定义cocoapods库
date: 2021-10-13 15:17:37
categories: [iOS]
tags:
---
## 1、本地创建pod库
创建名为SSExtension的pod库

```
$ pod lib create SSExtension
```

## 2、添加库文件
将库文件放入 `SSExtension/Classes` 文件夹里

cd 进 `Example` 路径下执行 `$ pod install `，执行完成后可见在工程中看到加入的文件。

## 3、将创建的库用git推到github上
cd 到 SSExtension 目录下执行命令

```
$ git init
$ git remote add origin git@github.com:ViiCat/SSExtension.git
$ git add .
$ git commit -m'commit'
$ git push origin master 
```
(ps: 若报 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'github.com:ViiCat/SSExtension.git' 说明，远程库有已存在文件，可用 `$ git push -f origin master` 进行强制覆盖)

## 4、注册 CocoaPods Trunk
用邮箱注册，注册成功会有邮件返回

```
$ pod trunk register luemark@live.com
```

## 5、发布自定义库
cd 到 SSExtension 目录 执行

```
$ pod trunk push SSExtension.podspec --verbose
```
如果有警告就用

```
$ pod trunk push SSExtension.podspec --verbose --allow-warnings
```
直到显示

<img src="/images/cocoapods.jpg">

就算成功了

## 总结
.podspec 配置里的 `s.version = '1.0.1'` 版本号，必须和github上打的tag标签版本一致，否则会出现pod install不下来。
简单来说操作步骤就是：

1、新建pod库 -> 2、添加文件到`Class`目录，并编辑`.podspec`配置 -> 3、把pod库上传到github并打`tag`版本 -> 4、执行`pod trunk push SSExtension.podspec --verbose --allow-warnings`将库发布

# git 相关

打标签

```
$ git tag 0.1.0 
$ git push --tags 			// 本地标记推送所有标签
$ git push origin master    	// 推到远程
$ git tag 					// 查看标签

$ git tag -d 0.1.0			// 删除标签

```

