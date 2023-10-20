# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux系统开发

### 自定义开机logo(基于命令行)

<img width="416" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/8d1e881a-73df-4ac8-b5cc-9d9df493ce1f"><br>
- /etc/issue & /etc/motd：
- motd = message of to day（布告栏）
- 登陆和欢迎信息控制

      语法格式：
      \d		本地端时间的日期
      \l 		显示第几个终端机接口
      \m 		显示硬件等级 (i386/i486/i586/i686…)
      \n 		显示主机的网络名称
      \o 		显示 domain name
      \r 		显示操作系统版本 (相当于 uname -r)
      \t 		显示本地端时间的时间
      \s 		显示操作系统名称
      \v 		显示操作系统版本

- 登录前，编辑 **/etc/issue**
- 登录后，编辑 **/etc/motd**

### 自定义开机启动项（基于命令行）

登录前开机启动项，编辑 **/etc/rc.local** 文件：<br>
- 1.打开 /usr/lib/systemd/system/rc-local.service 文件，添加下面内容：

      [Install]
      WantedBy=multi-user.target
      Alias=rc-local.service

- 2.重新加载文件:

      systemctl daemon-reload

- 3.在 /etc/ 路径下创建 **rc.local**文件，并加入下面内容：

      #!/bin/sh -e
      #
      # rc.local
      #
      # This script is executed at the end of each multiuser runlevel.
      # Make sure that the script will "exit 0" on success or any other
      # value on error.
      #
      # In order to enable or disable this script just change the execution
      # bits.
      #
      # By default this script does nothing.

      # 这里放要执行的命令or执行shell脚本的语句

      exit 0

- 4.如果用户默认运行环境在 /bin/bash 下，则应修改 #!bin/sh -e为 #!bin/bash -e

      查看用户运行环境：/etc/passwd
  
<img width="245" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/288925c8-dd6f-4cc9-9465-d5c2655a28ad"><br>

- 5.修改权限为可执行：

      chmod 755 /etc/rc.local

- 6.重启rc服务：

      systemctl restart rc-local.service

- 7.设置开机自启动：

      systemctl enable rc-local

登录后开机启动项，编辑 **/etc/profile.d/** 目录下文件：<br>
写好的 **shell脚本(.sh文件)** 放到目录 **/etc/profile.d/** 下<br>
系统每次启动且登录后会自动执行该目录下所有shell脚本<br>

### 自定义终端命令（基于命令行）

Linux端的任何命令都可以替换成其他的字符串来代替<br>
Linux同时还可借助 **shell脚本** 或者 **python脚本** 来实现命令的自定义<br>

替换方法 alias：<br>

	alias指令：			设置指令别名
	alias语法格式：	alias 自定义指令名='指令'
	
	alias：				  查看当前所有的别名设置
	alias 指令名：		查看具体一条指令的别名
	unalias 指令名：	删除指定别名

自定义命令：<br>
- 1.打开文件

      vim /etc/bashrc	#所有用户都生效

- 2.文末添加对应指令别名

      alias [自定义命令]=[原生命令or其组合or shell脚本 or python脚本]

- 3.生效配置文件

      source /etc/bashrc

自定义命令永久生效：<br>
- 1.结合开机启动项，写好的 shell脚本(.sh文件) 放到目录 /etc/profile.d/ 下
- 2.Shell脚本执行 source /etc/bashrc 设置配置文件

版本信息输出指令：<br>

    cat /proc/version  	#查看版本信息
    uname -a   			#查看版本和内核
