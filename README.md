# 智能门锁项目标准

项目主要由以下几部分构成

## UltraLock.Hardware(C//STM32)

### 要求
门锁单片机内烧录的程序
1. 通过串口与计算机通讯，接收开门、关门指令，发送NFC卡ID；
2. 通过控制继电器控制门开关。

## UltraLock.Drive(?)

门锁驱动程序，将API暴露给其它程序调用。应当编译为DLL。

1. 暴露API，通过串口与单片机通讯，发送开门、关门指令；
2. 鉴权功能，获取NFC卡ID，并与数据库进行对比，认证成功开门；
3. 暴露API，添加删除NFC卡ID。

## UltraLock.Server(C#/ASP.NET Core/.NET5)

门锁Web API提供程序，通过HTTP API更方便的与其它程序交互

1. 身份认证，拥有一个或多个管理账户，能够添加令牌、NFC卡ID、bot QQ；端点为：
  1. 账户 `v1/Admin/Account`
  2. 令牌操作 `v1/Admin/Token`
  3. NFC卡ID `v1/Admin/Card`
  4. bot QQ `v1/Admin/Bot`
2. 身份认证，非管理员用户用于登陆并获取令牌；端点为：
  1. `v1/Member`
3. 开门关门的HTTP API，端点为
  1. `v1/Door`

## UltraLock.Client.Web （HTML/vuejs）

门锁客户端网页端，用于管理用户和用户网页登陆
1. 用户登陆后通过按钮执行开门操作
2. 管理用户登陆后能够管理普通账户，令牌、卡ID、bot QQ等

## UltraLock.Client.Android (Kotlin)

安卓应用程序，用于用户快速开门，登陆后应保存用户Token，过期后再刷新

## UltraLock.Client.Qbot (python/mirai/python3.9)

QQ 机器人，用于在群里供群友开门

1. 自定义设置指令、响应的群号
2. 支持发送指令开门（鉴权使用Web API签发的令牌）
