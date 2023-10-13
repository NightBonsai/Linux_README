# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux网络编程

### *服务器常用Linux，客户端常用Windows：Linux开源免费，安全性高*

### Linux网络基础：
网络三要素：<br>
- IP地址：网络中查找对方计算机
- 端口号：确定计算机中某一个应用程序 10000以下系统+默认程序使用
- 通信协议：双方共同约定和遵循的协议(数据打包、解包规则)

- 计算机网络体系结构：详见计网
- TCP/IP协议族：详见计网

### Linux网络编程：
- socket概述：

      一套网络通信程序的API函数标准
      linux中的网络编程通过socket接口实现；
      socket既是一种特殊的IO，也是一种文件描述符

- 基于流套接字(socket)的编程流程：

      socket函数：          网络初始化，判断是否可以搭建网络
      bind函数：            绑定端口和IP地址(其中要将sockaddr_ in结构体转化成sockaddr)
      sockaddr_ in结构体

        .sin_ sin_ family：   网络连接协议族
        .sin_ _addr.s_ _addr：本地联网IP
        .sin_ port：          开放服务器端口，一般10000以上；用htos函数将主机字节顺序转换为网络字节顺序，防止数据由于大小端模式的不同而出错

      listen函数：          监听是否有户上线
      accept函数：          阻塞函数,等待用户连接
      connect函数：         客户端函数，参数类似bind函数，客户端连接服务器；在qt中使用linux socket函数的connect：使用::connect()即可解决
      read|write函数：      客户端和服务器端之间数据的读入写出

### socket-IO复用技术：
- 端口复用，避免出现address already be used:

      int optval= 1; 
      setsockopt(	socketfd，SOL_SOCKET，SO_REUSEADDR，(const void*)&optval，sizeof(optval))；

- IO复用技术：
- <img width="240" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/cef826d6-b1c5-4921-bfae-343e5a254022">
- <img width="397" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/bf1d0114-fa7d-4a6a-a6f5-7c35de7edd48">

**Epoll = 事件列表 + 就绪列表**<br>
**Linux 网络编程API里的epoll只有eventpoll**<br>

    struct epoll_event：epoll事件结构体
    int epoll_create(int size);                                                               //创建epoll
    int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event);                       //epoll事件队列添加or删除事件
    int epoll_wait(int epfd, struct epoll_event* events, int maxevents, int timeout);					//等待事件队列事件发生

**epoll解决同时接收N个客户端连接fd问题**<br>
**但无法解决任务并发，客户端排队问题**<br>

### 线程池技术：见网络小总结
### 高并发服务器架构：见网络小总结
