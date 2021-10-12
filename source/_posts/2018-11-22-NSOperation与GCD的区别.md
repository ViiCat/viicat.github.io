---
layout: post
title: "【NSOperation】与 GCD的区别"
date: 2018-11-22 08:00:00 +0800
categories: [iOS]
---

### NSOperation 与 GCD区别
1、GCD仅仅支持FIFO队列(先进先出)，NSOperation可以被重新设置优先级。

2、NSOperationQueue支持KVO，意味着可以观察任务的执行状态。

3、NSOperationQueue可以取消已经设定准备执行的任务（已经开始的任务无法阻止），GCD无法停止已经加入队列的任务（可以实现，但需要加许多复杂代码）

