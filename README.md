# Jprofiler监控远程Tomcat

## 准备
[Jprofiler下载地址](https://www.ej-technologies.com/download/jprofiler/files)，需要同时安装:
- Linux端jprofiler服务端
- windows端jprofiler客户端

需要注意的是Linux端和Windows端的版本需要保持一致。建议使用10.0以下版本，因为目前10.X版本破解注册码不完善。


## 安装

- 下载Linux版Jprofiler服务端,放到/opt下,直接解压,这里以jprofiler9.2为例。
    ```bash
    tar -zxvf  jprofiler_linux_9_2_1.tar.gz
    ```

    解压完成后，可以看到/opt/jprofiler9

- 配置tomcat启动服务。

    进入tomcat的bin目录下，将startup.sh复制一份并且改名为startup_jprofiler.sh。在startup_jprofiler.sh中exec指令前添加以下2行：
    
    ```
    CATALINA_OPTS="-agentpath:/opt/jprofiler9/bin/linux-x64/libjprofilerti.so=port=8849,nowait $CATALINA_OPTS"
    export CATALINA_OPTS
    ```

    其中agentpath就是服务端所在的启动位置，这里我们是放在/opt/jprofiler9下。这里port就是我们jprofiler的远程监控端口，默认8849，可自由指定，在接下来的监控中会用到该端口,不过建议不要用80,8080等常规通用接口。

- 安装windows客户端
    
    因为jprofiler是收费软件，这里我们进行破解，有能力建议支持正版.以下是注册码，任选一使用。其中用户名和公司名任意填写。
```
L-Larry_Lau@163.com#23874-hrwpdp1sh1wrn#0620 
L-Larry_Lau@163.com#36573-fdkscp15axjj6#25257 
L-Larry_Lau@163.com#5481-ucjn4a16rvd98#6038 
L-Larry_Lau@163.com#99016-hli5ay1ylizjj#27215 
L-Larry_Lau@163.com#40775-3wle0g1uin5c1#0674 
```
   
## 使用

一切准备就绪，接下来，我们就开始使用Jprofiler来监控Tomcat程序性能。

-  Session=>Integration Wizards=>New Remote Integration
-  选择远程服务器版本,本案例选择Linux X86/AMD64，Next
-  选择JVM版本，Next
-  Next
-  指定需要监控tomcat服务的服务器地址，Next
-  输入Linux服务器上jprofiler的安装目录，Next
-  指定startup_jprofiler.sh中配置的端口，Next
-  Next，直到完成
