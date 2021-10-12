---
layout: post
title: "【ReactiveCocoa】 for Swift and OC"
date: 2018-12-06 08:00:00 +0800
categories: [iOS, Swift]
---

### ReactiveCocoa for Swift
<a href = "https://github.com/ReactiveCocoa">传送门</a>
>`ReactiveCocoa` 主要集中在Swift和UI层上，将原来基于RAC面向UI层扩展库<a href "https://github.com/RACCommunity/Rex">Rex</a>合并进了RAC
>
>`ReactiveSwift` RAC中只和Swift平台相关的核心代码单独抽取生成新框架，可以在其他平台上被使用，不局限在CocoaTouch 和 Cocoa 中
>
>`ReactiveObjC` 针对OC代码的库
>
>`ReactiveObjCBridge` OC 迁移到 Swift 过程中，可能使用Swift 调用 RAC2 中基于 OC 写的 API

如项目是纯 Swift ，使用 ReactiveCocoa。但 RAC 依赖于 ReactiveSwift ，等于引入了2个库

如项目是纯 OC ，使用ReactiveObjC。这个库包含RAC 2 的全部代码

如项目是 Swift 和 OC 混编，需引入 ReactiveCocoa 和 ReactiveObjCBridge 。但是ReactiveObjCBridge 依赖于 ReactiveObjC ，等于引入了4个库


参考:

https://www.jianshu.com/p/dfcf0cce37e6

https://www.jianshu.com/p/3a56d10e99a7

https://www.jianshu.com/p/4554fd087bed