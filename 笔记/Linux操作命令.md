# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux操作命令

### Linux切换root用户：
		
    设置root用户密码：  sudo passwd root
		  设置root用户密码
		切换root用户：      su root
		  输入密码切换
		退出root用户：      exit

### 常用快捷键：

    挂起终端进程-终端：			ctrl+z
    强制中断程序-终端：			ctrl+c
    清屏命令-终端：				clear
    查看隐藏文件：				  ctrl+h
    查看隐藏文件-终端：			ls -a
    查看文件详细信息-终端：	ls -l
    Linux重启-终端：			  reboot
    Linux关闭-终端：			  shutdown -h now
	
### 文件操作：
		
    切换目录：			        cd 要切换到的目录（.当前路径 ..上一级路径 ~home路径）
		输出目录下所有文件信息：ls（输出文件名） or ll（输出文件详细信息）
		文件创建：			        touch
		文件拷贝：			        cp 文件 目标目录
		文件移动：			        mv 文件 目标目录
		文件删除：			        rm 文件 目标目录
		文件夹创建：		        mkdir 文件夹
		文件夹删除：		        rmdir 文件夹
		删除非空目录：		      rm -R 目录
		查看文本内容：		      cat 文件（瞄一眼）
		查看系统磁盘使用情况：  df -hl

### Linux设备&进程指令：
		
    ps -aux：    查看任务管理器
		pstree：     查看进程树状图
		
### 文件权限管理：

    chmod：给创建文件的用户赋予更多权限r-4 w-2 x-1 u-该文件拥有者g-该档案拥有者同组成员o-其他人

### 用户&组的增删改查：

    创建用户：						        useradd xxx (创建时会自动创建同名组) ;
    创建组：						          groupadd xxx;
    用户添加到组：					      useradd 用户名 组;
    
    root修改普通用户口令/密码：		passwd 用户名
    普通用户修改口令/密码：			  passwd
    
    删除用户：						        userdel 用户名 组名;
    删除用户及其组：				      userdel -r 用户名
    删除组：						          groupdel 组名;

### 修改文件所属用户&组

    chown 所属用户:所属组 文件名

### 删除用户
    
    deluser -remove-home 用户名

### Vim操作：

    安装：                       apt install vim
    Vim创建or打开文件进行编辑：   vim 文件
    进入insert编辑模式：         点i
    编辑完成退出insert模式：     Esc
    保存退出文件：              :wq
    退出不保存文件：            :q!
    Shell Bash：通配符，上下键记忆命令，Tab自动补全，输出/入重定向：>,>>,<,	管道：I
    
<img width="416" alt="image" src="https://github.com/NightBonsai/Linux_README/assets/107353989/8ce29efb-169f-4387-8b9c-8de50c484672"><br>


### Shell脚本语言：
见后<br>
	
### gedit操作：
工具，类似Windows的记事本；<br>

### tar解压工具操作：

    tar –xvf 压缩包名：	*.tar
    tar –xzf 压缩包名：	*.tar.gz or *.tgz
    tar -xf  压缩包名：	*.tar.xz
    tar –xjf 压缩包名：	*.tar.bz2
    tar –xZf 压缩包名：	*.tar.Z

### tar压缩工具操作：
	
    tar -zcvf 压缩包名.tar.gz DirName	# 将DirName和其下所有文件压缩为tar.gz
	  tar -cvf  压缩包名.tar DirName		# 将DirName和其下所有文件打包tar

### Linux文件IO指令：
- 终端指令—man 2/3... 指令名：查看API使用手册—Linux Programmer's Manual

      umask()： 设置权限掩码，默认0022	rwx421——rwxrwxrwx777
	    perror()：输出报错信息，头文件stdio.h中
	    open()：  打开文件
	    close()： 关闭文件
	    write()： 文件写入数据
	    read()：  文件读取数据
		
### 获取读写数据大小：
		
    strlen—针对纯文本文件：txt cpp h
		sizeof—针对二进制文件：zip mp4 mp3
		复制拷贝文件的时候推荐：write长度就是read的返回值
