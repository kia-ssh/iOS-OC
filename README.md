
# iOS OC简单整理

[TOC]

## OC语言基本
编码及调试需要了解的基本机制
- runloop
- runtime
- arc
- kvo
- 消息传递、转发

编码过程错误警告查看：
> https://clang.llvm.org/docs/DiagnosticsReference.html

## sdk 开发较多用到
- 可执行文件格式(可执行文件类unix都基本类似)
- mach-o的一些存在形态 .a 、.o 、.framework、.dylib了解
- dyld加载机制，dyld注入库及加载库监听 
>`<mach-0/dyld.h>`

##  OC 开源库整理

| 库                                                                    | 说明                           |
| :-----------------------------------------------------------------    | :---------------------------- |
| [AFNetWorking](https://github.com/AFNetworking/AFNetworking)          | iOS著名网络库                   |   
| [CocoaAsyncSocket](https://github.com/robbiehanson/CocoaAsyncSocket)  | 异步socket                     |
| [KVOController](https://github.com/facebookarchive/KVOController)     | iOS 安全的KVO库
| [WCDB](https://github.com/Tencent/wcdb)                               | 微信搞的iOS数据库框架
| [YYModel](https://github.com/ibireme/YYModel)                         | 模型框架
| [SDWebImage](https://github.com/SDWebImage/SDWebImage)                | 图片加载框架
| [ReactivieCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)      | 响应式编程框架
| [Reachability](https://github.com/tonymillion/Reachability)           | 网络状态监控


## iOS 逆向相关
看了这两个介绍博客都挺全的
> https://www.jianshu.com/p/58a6310ece37
> https://www.jianshu.com/p/2410fe5c6b96

### 辅助查看工具: 
- hopper disassembler
- Mach-O View

### 命令：
- nm
- otool

## crash

> [官方文档分析crash](https://developer.apple.com/documentation/xcode/diagnosing-issues-using-crash-reports-and-device-logs)

常用crash分析符号化 
- xcrun atos 命令分析
- symbolicatecrash

### 常见crash大概理一下


OC语言机制、基本语法容易出现
- unrecognized selector. 写法问题，了解OC消息发送体系即可。
> `<objc/message.h>`  ***objc_msgSend(...)***
- 数组越界
- 集合传nil
- KVO监听和溢出不均衡
- 子线程UI(你SDK应该不涉及)
- 语法导致的野指针（了解ARC， 常见为property修饰符，常见copy、retain、asssign等错用. ）


内存问题
- 野指针 (多见多线程野指针)
- 内存对齐 （多见类型问题）
- 内存溢出 (大量leak或一次性加载大内存内容导致)
