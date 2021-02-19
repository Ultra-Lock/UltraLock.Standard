# 智能门锁项目标准

项目主要由以下几部分构成

## UltraLock.Hardware(C//STM32)

### 负责

[@nidbCN](https://github.com/orgs/Ultra-Lock/people/nidbCN)

### 要求
门锁单片机内烧录的程序
1. 通过串口与计算机通讯，接收开门、关门指令，发送NFC卡ID；
2. 通过控制继电器控制门开关。

## UltraLock.Server(C#/ASP.NET Core/.NET5)

门锁Web API提供程序，通过HTTP API更方便的与其它程序交互

### 负责

[@nidbCN](https://github.com/orgs/Ultra-Lock/people/nidbCN)
[@YeLingLiTian](https://github.com/orgs/Ultra-Lock/people/YeLingLiTian)

### 要求

1. 身份认证，拥有一个或多个管理账户，能够添加令牌、NFC卡ID、bot QQ；端点为：
  1. 账户 `v1/Admin/Account`
  2. 令牌操作 `v1/Admin/Token`
  3. NFC卡ID `v1/Admin/Card`
  4. bot QQ `v1/Admin/Bot`
2. 身份认证，非管理员用户用于登陆并获取令牌；端点为：
  1. `v1/Member`
3. 开门关门的HTTP API，端点为
  1. `v1/Door`
4. 通过串口发送开门关门指令
5. 通过串口获取NFC卡ID，鉴权后开门

### 资料

[CnBlog:.Net Core 跨平台应用使用串口、串口通信 ，可能出现的问题、更简洁的实现方法](https://www.cnblogs.com/whuanle/p/10499498.html)  
[MSDN:教程：ASP.NET Core 入门](https://docs.microsoft.com/zh-cn/aspnet/core/getting-started/?view=aspnetcore-5.0&tabs=windows)  
[哔哩哔哩:ASP.NET Core 3.x 构建 RESTful API（已完结）](https://www.bilibili.com/video/BV1XJ411q7yy)

## UltraLock.Client.Web （HTML/vuejs）

### 负责

[@YeLingLiTian](https://github.com/orgs/Ultra-Lock/people/YeLingLiTian)

### 要求

门锁客户端网页端，用于管理用户和用户网页登陆
1. 用户登陆后通过按钮执行开门操作
2. 管理用户登陆后能够管理普通账户，令牌、卡ID、bot QQ等

### 资料

[Vue.Js](https://cn.vuejs.org/v2/guide/)
[Vuetify](https://vuetify.cn/zh-Hans/getting-started/quick-start/)

## UltraLock.Client.Qbot (python/mirai/python3.9)

QQ 机器人，用于在群里供群友开门

### 负责

[@chengjuzi](https://github.com/orgs/Ultra-Lock/people/chengjuzi)

### 要求

1. 自定义设置指令、响应的群号
2. 支持发送指令开门（鉴权使用Web API签发的令牌）

### 资料

1. [Github:iTXTech/mirai-console-loader](https://github.com/iTXTech/mirai-console-loader)
2. [Github:GraiaProject/Application](https://github.com/GraiaProject/Application)
3. [Requests Docs](https://cn.python-requests.org/zh_CN/latest/)

## UltraLock.Client.Android (Kotlin)(可选)

安卓应用程序，用于用户快速开门，登陆后应保存用户Token，过期后再刷新
