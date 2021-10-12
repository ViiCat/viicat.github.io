---
layout: post
title:  "【SublimeText】插件安装"
date:   2018-10-19 16:41:24 +0800
categories: [IDE, SublimeText]
---

## 下载安装
下载地址: https://www.sublimetext.com/3

## 安装 Package Control
SublimeText 插件都要借助这个工具来安装，打开SublimeText点击顶部菜单View -> Show Console（或者使用快捷键command + ~），会弹起一个控制台，输入下面代码：
```
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

或粘贴 https://packagecontrol.io/installation 里面代码，等待安装完成。

## 安装插件
点击顶部菜单SublimeText -> Preferences -> PackageControl 或通过快捷键Command + Shift + P 打开PackageControl 来安装需要的插件

参考:https://www.cnblogs.com/im5437/articles/8119906.html