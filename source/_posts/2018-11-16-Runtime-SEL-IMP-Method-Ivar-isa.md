---
layout: post
title: "【Runtime】SEL、IMP、Method、Ivar、isa、Cache"
date: 2018-11-16 08:00:00 +0800
categories: [iOS, Objective-C]
---

### Runtime 基本类型
SEL：选择器指向一个C String

```
typedef struct objc_selector *SEL;
```
<br/>

IMP：指向实际执行函数体的函数指针

```
#if !OBJC_OLD_DISPATCH_PROTOTYPES
typedef void (*IMP)(void /* id, SEL, ... */ ); 
#else
typedef id (*IMP)(id, SEL, ...); 
#endif
```
<br/>

Method：指向方法的指针
```
typedef struct objc_method *Method;
```

```
struct objc_method {
    SEL method_name                                          OBJC2_UNAVAILABLE;
    char *method_types                                       OBJC2_UNAVAILABLE;
    IMP method_imp                                           OBJC2_UNAVAILABLE;
} 
```
<br/>

Ivar：成员变量指针

```
typedef struct objc_ivar *Ivar;
```

```
struct objc_ivar {
    char *ivar_name                                          OBJC2_UNAVAILABLE;
    char *ivar_type                                          OBJC2_UNAVAILABLE;
    int ivar_offset                                          OBJC2_UNAVAILABLE;
#ifdef __LP64__
    int space                                                OBJC2_UNAVAILABLE;
#endif
}    
```
<br/>

Property：属性指针

```
typedef struct objc_property *Property;
typedef struct objc_property *objc_property_t;//这个更常用
```

isa：指向类的指针；id：
<br/>

```
typedef struct objc_object *id;
```

```
struct objc_object {
    Class isa  OBJC_ISA_AVAILABILITY;
};
```
<br/>

Cache

每当实例对象接收到消息时，它不会直接在isa指针指向的类方法列表里遍历查找能响应的方法，因为每次查找效率都太低，而优先在Cache中查找。
Runtime系统会把被调用的方法存进Cache里，就像计算机组成原理一样CUP绕过主存先访问Cache一样。

```
typedef struct objc_cache *Cache
```

```
struct objc_cache {
    unsigned int mask /* total = mask + 1 */                 OBJC2_UNAVAILABLE;
    unsigned int occupied                                    OBJC2_UNAVAILABLE;
    Method buckets[1]                                        OBJC2_UNAVAILABLE;
};

```
<br/>
<strong>参考文章</strong>

https://blog.csdn.net/Hello_Hwc/article/details/49682857