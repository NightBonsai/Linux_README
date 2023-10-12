# C/C++_programmin

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux基础

### 1.Ubuntu16.04换国内源：http://t.zoukankan.com/masbay-p-10887571.html

### 2.Linux Qt cannot find -lGL错误完美解决方案：
		
    Qt 找不到 OpenGL 的动态链接库（libGL.so）
		Qt 默认在 /usr/lib/ 目录下查找动态链接库，但是很多 Linux 发行版将 OpenGL 链接库放在其它目录；只要我们把 libGL.so 拷贝到 /usr/lib/ 目录，或者在 /usr/lib/ 目录下为 libGL.so 创建一个链接，就能解决问题。显然第二种办法更好
		
    #查找 libGL 所在位置
    [root@localhost ~]# locate libGL
    /usr/lib64/libGL.so
    /usr/lib64/libGL.so.1
    /usr/lib64/libGL.so.1.2.0
    /usr/share/doc/mesa-libGL-9.2.5
    /usr/share/doc/mesa-libGL-9.2.5/COPYING
    #创建链接
    [root@localhost ~]# ln -s /usr/lib64/libGL.so.1 /usr/lib/libGL.so

    Linux 系统中可能存在多个版本的 libGL.so，为任意一个版本创建链接即可。普通用户没有权限创建链接，所以我使用了 root 用户；完成以上操作，再次启动 Qt，然后编译或者运行，就不会出现“cannot find -lGL”错误了。
	
 ### 3.使用VS2019进行Linux远程开发中文乱码问题：
<img width="354" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/bed508a9-33b7-459c-8413-b27fb0c062c2"><br>

### *4.服务器常用Linux，客户端常用Windows：因为Linux开源免费，安全性更高*；

### 5.Linux框架结构：
- 裸机+内核Kernel+外核Shell（向上提供接口）+应用程序+外围工具（应用程序）

### 6.Linux设备管理：
所有设备都能看做是特殊的文件

### 7.Linux文件：
- 后缀为*：可执行文件
- 前缀为d：文件夹
- 前缀为-：文件

      /home：		    主目录 ，例：home/user = ~user
      /root：		    系统管理员的主目录

      /bin：		    存储Linux常用命令，二进制可执行命令
      /boot：		    系统盘，存储操作系统引导程序
      /dev：		    Linux系统中使用的外部硬件设备映射文件
      /etc：		    系统管理&配置文件
	      /etc/passwd		    用户信息
        /etc/shadow		    用户密码(已加密)
        /etc/group 		    组信息
        /etc/rc.d			    启动的配置文件&脚本
        /etc/profile.d/		系统启动后自动执行该目录下所有shell脚本
      /lib：		    标准程序设计库/动态连接共享库	≈ Windows .dll文件
      /lost+found： 存储系统强制关闭时丢失的文件
      /mnt：		    分区的挂载点
      /proc：		    虚拟目录，系統内存的映射，可获得系统信息
      /usr：		    用户很多应用程序&库都放在这

<img width="416" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/e83d6eb5-ef07-4d67-84f0-5fb9560bc13b"><br>


### 8.Linux用户类别:
- root：最高权限;
- owner：实际拥有文件的用户; 
- group：用户组; 
- world：其他用户；

### 9.Linux文件权限位：
- 共10位：  r读w写x执行-没有该权限
- 文件类型：普通文件-、目录d、链接文件(快捷方式)l 
- 第一位:文件类型；后三位: owner的权利；后三位: group的权利；后三位: word的权利;

### 10.LinuxCRT中文乱码问题：
在windows里面记事本方式打开cpp，另存为UTF-8编码，在ubuntu里面打开就不会乱码了；再放到ubuntu里面去<br>

### 11.用CRT远程连接Linux开发：
服务器不常在身边，要在服务器的操作系统上进行开发就必须远程连接<br>
CRT远程连接使用UTF-8编码方式<br>
	
### 12.静态库&共享库：
- 静态库（.a）：      程序在编译链接的时候把库的代码链接到可执行文件中
- 共享库（.so或.sa）：程序在运行的时候才去链接共享库的代码，多个程序共享使用库的代码

### 13.Linux系统调用内核函数 & API函数库调用函数：
- 系统调用：       直接请求操作系统内核服务，执行代码效率更高；每种操作系统内核函数各不相同，具有局限性
- API函数库调用：  封装在程序内的函数；调用兼容性、可移植性更好；调用开销更小；

### 14.Linux清理文件缓存：
清理 /home/xxxx/.cache/vmware/drag_and_drop 文件夹下所有数据


