# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux系统启动引导

### 基于System V init启动方法
- **1.内核引导**：<br>

      1.1.BIOS开机自检：  按照BIOS中设置的启动设备（硬盘）来启动，操作系统接管硬件
	    1.2.读入内核文件：  读入 /boot 目录下的内核文件
- <img width="250" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/061eac61-296e-4b2a-a936-8c15548e14fb">


- **2.运行init**：<br>
**0号进程（init进程）**：所有进程的祖宗，父进程<br>
**0号进程需要运行的程序（许多程序需要开机启动）**："守护进程"（daemon）<br>
运行级别（runlevel）：<br>
Linux允许为不同的场合，分配不同的开机启动程序<br>
启动时根据"运行级别"，确定要运行哪些程序。<br>

      2.1.内核被加载后，第一个运行的程序便是/sbin/init，该程序会读取0号进程
      2.2.运行0号进程：读取配置文件 /etc/inittab
      2.3.0号进程运行程序：依据运行级别运行程序

- <img width="304" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/cc329543-6c47-4af2-bcbc-ef27f95e1fa5"> <img width="412" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/e8acb66c-c00c-4492-a54f-579183330f7a">

Linux系统有7个运行级别(runlevel)：<br>

    运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动
    运行级别1：单用户工作状态，root权限，用于系统维护，禁止远程登录
    运行级别2：多用户状态(没有NFS)
    运行级别3：完全的多用户状态(有NFS)，登录后进入控制台命令行模式
    运行级别4：系统未使用，保留
    运行级别5：X11控制台，登录后进入图形GUI模式
    运行级别6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动

- **3.系统初始化**：<br>
init的配置文件中 si::sysinit:/etc/rc.d/rc.sysinit<br>
**调用执行 /etc/rc.d/rc.sysinit**<br>
**rc.sysinit**：<br>
一个bash shell的脚本，完成一些系统初始化工作<br>
是每一个运行级别都要首先运行的重要脚本<br>

	    l5:5:wait:/etc/rc.d/rc 5

      以5为参数运行  /etc/rc.d/rc  Shell脚本
	    该脚本会执行  /etc/rc.d/rc5.d/  目录下的所有 rc启动脚本：
		      是一些连接文件，而不是真正的rc启动脚本
		      真正的rc启动脚本：/etc/rc.d/init.d/ 目录下

每个运行级中将运行哪些守护进程，用户可以通过chkconfig或setup中的"System Services"来自行设定<br>
- <img width="416" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/100833c3-0e19-4649-aa4f-84418811a2c3">

- **4.建立终端**：<br>
rc执行完毕，返回init<br>
基本系统环境已经设置好了，各种守护进程也已启动<br>
init接下来会打开6个终端，以便用户登录系统，Linux预设提供了六个命令窗口终端机让我们来登录<br>

      1:2345:respawn:/sbin/mingetty tty1
      2:2345:respawn:/sbin/mingetty tty2
      3:2345:respawn:/sbin/mingetty tty3
      4:2345:respawn:/sbin/mingetty tty4
      5:2345:respawn:/sbin/mingetty tty5
      6:2345:respawn:/sbin/mingetty tty6
	
- **5.用户登录系统**：<br>

      （1）命令行登录
      （2）ssh登录
      （3）图形界面登录

Linux 账号验证程序login：<br>

    接收 mingetty 传来的用户名作为用户名参数。
    对用户名进行分析：
        如果用户名不是 root，且存在 /etc/nologin 文件，输出 nologin 文件内容后退出
        用来系统维护时防止非root用户登录
    只有/etc/securetty中登记了的终端才允许 root 用户登录
    如果不存在这个文件，则 root 用户可以在任何终端上登录。
    /etc/usertty文件用于对用户作出附加访问限制，如果不存在这个文件，则没有其他限制。

- <img width="416" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/f2455197-b357-4704-b428-6d1867503d31">
