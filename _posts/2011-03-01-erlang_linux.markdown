---
layout: post
title: Erlang Linux
category: Erlang
---




## linux查看进程的命令

`ps aux`

a -- 显示系统中所有用户的进程

u -- 输出进程的用户所属信息

x -- 显示没有控制台的进程


## 查找服务名为erlang的进程

`ps aux | grec erlang`



## linux查看系统监听的服务

｀netstat -lna｀


l -- 当前系统监听的端口信息

n -- 端口按照端口号来显示

a -- 所有的服务


## erl 命令参数介绍

*boot

指定启动文件，默认值: $ROOT/bin/start.boot
*s Mod Func Arg1,Arg2
    
init调用的方法，

*setcookie Cookie

设置cookie

*name Name

让erlang运行时系统运行在Name结点上， Name的形式 Name@Host

*config Config

明确configuration文件

*noshell

不用对话界面

*pa path

path为绝对路径，指导程序的启动路径

｀erl -noshell -s hello start -s init stop｀




## erlang应用程序

有一个application callback module,应用程序的启动和终止的方法。app_name.erl

应用程序的描述文件 application resource file，记录应用程序的基本信息，app_name.app文件

其内容如下：
{application,app_name,
    [{description,"Just Sample"},
    {vsn,"0.01"},
    {modules,[]},
    {registered,[]},
    {mod,{app_name,[]}},
    {env,[]},
    {applications,[kernel,stdlib,crypto]}
    ]
}


modules -- 应用程序执行完start后，要运行的start的module列表

mod -- 应用程序的入口，这个module的start stop脚本

applications -- 应用程序运行之前，必须启动或运行的应用

application master进程是应用程序的主进程，控制着应用程序的执行