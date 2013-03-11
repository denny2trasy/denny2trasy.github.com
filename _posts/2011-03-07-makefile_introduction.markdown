---
layout: post
title: What is makefile?
---


## linux下用make工具编译程序，关键是makefile文件。

make命令有4个可选参数
    make [flags] [macro] [definitions] [targets]

    flags选项

        -f file 指定file为描述文件
        -s 沉默模式，执行之前不输出相应的命令行信息
        -r 禁止试用build-in规则
        -n 非执行模式，输出所有执行命令，但是不执行
        -t 更新目标文件
        -q make操作将根据目标文件是否已经更新返回0或者非0
        -p 输出所有宏定义和目标文件描述
        -d Debug模式，输出有关文件和检测时间的详细信息
        -c dir 在读取makefile之前改变到指定的目录上
        -h help文档
        -w 在处理makefile之前和之后，都显示工作目录
        …

    macro
    
        1。可以在makefile文件中定义宏
            OBJECTS=filea.o fileb.o   (定义宏)
            $(OBJECTS)        (应用宏)
        2。在命令行中输入宏定义
            make "LIBS=-LL -LS"    命令行中输入宏

    targets
    
        用来指定make命令要编译的目标文件，并且允许同时定义编译多个


make all  编译所有的目标

make clean 清除之前所编译的可执行文件及目的文件

make distclean 除了清除可执行文件和目标文件外，同时把makefile文件也清除掉

make install 将程序安装到系统中


## gdb是用来调试c和c++程序的强力调试器



## wc 命令用来显示指定文件中 行数，字数 字节数

    $ wc -lwc file1 file2


## Erlang/OTP(Open Telecom Platform) 是包装在Erlang中的一组程序

    三种机制

        行为机制(behaviours)
            gen_server: 创建通用服务器，向多个客户端提供服务 
            gen_fsm:  有限状态机
            gen_event: 创建事件处理器和发报器
        应用行为(Application behavior)
        监测行为(Supervisor behavior)