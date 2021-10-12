---
layout: post
title: "【Runtime】+【Category】打印每个页面进入的时间"
date: 2018-11-16 08:00:00 +0800
categories: [iOS, Objective-C, Runtime]
---

#### 首先创建类别文件 New File -> Objective-C File -> File Type 选 Category

<strong>接下来编辑`.m`文件</strong>：

`UIViewController+Category.m`

<strong>导入runtime文件头</strong>：

```
#import <objc/runtime.h>
```

在`.m`文件里写入如下代码：

```
+ (void)load {
    
    ///仅执行一次
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        
        //获得方法的实例
        Method wda = class_getInstanceMethod([self class], @selector(viewDidAppear:));
        Method swizzlingWda = class_getInstanceMethod([self class], @selector(swizzling_viewDidAppear:));
        
        //避免源SEL没有实现IMP的情况
        BOOL isAdd = class_addMethod([self class], method_getName(swizzlingWda), method_getImplementation(swizzlingWda), method_getTypeEncoding(swizzlingWda));
        
        if (isAdd) {
            class_replaceMethod([self class], method_getName(swizzlingWda), method_getImplementation(swizzlingWda), method_getTypeEncoding(swizzlingWda));
        } else {
            //关键,方法交换
            method_exchangeImplementations(wda, swizzlingWda);
        }
    });
}
```

加入需要替换成的方法：

```
- (void)swizzling_viewDidAppear:(BOOL)animated {
    //原因在此之前方法已经完成了交换
    //这句相当于调用-(void)viewDidAppear:(BOOL)animated; 
    [self swizzling_viewDidAppear:animated];
    
    //类名称
    const char *cName = class_getName([self class]);
    //系统时间
    NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
    formatter.dateFormat = @"yyyy-MM-dd HH:mm:ss";
    NSString *strTime = [formatter stringFromDate:[NSDate date]];
    NSLog(@"\nClass:%@\nTime:%@",[NSString stringWithUTF8String:cName],strTime);
}
```


Demo：
<a href="https://github.com/ViiCat/Demo">https://github.com/ViiCat/Demo<a/>
