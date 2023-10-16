# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux终端命令行

### 基础概念：
- 终端(Terminal)：字符输入输出设备；是一种特殊的文件，在/dev目录下；键盘输入会写这个文件；
- Shell：命令解释软件；解析输入字符，执行对应指令；fork + exec + wait加载别的可执行程序并运行；

### 终端Terminal和Shell的关系：
- shell的stdin、stdout和stderr 指向 terminal文件
- 键盘输入字符写入terminal文件，Shell通过stdin从terminal文件中读取输入字符

### 命令执行方式：
- Ubuntu默认使用Shell为bash

      打开终端 → 启动bash → bash接收终端文件的输入字符串

### Bash执行指令方式：
- 1.绝对路径执行：指定执行的命令脚本路径+命令文件（例：/home/bin/la.sh）
- 2.sh执行：用脚本对应的sh或bash来接着脚本执行（例 sh test.sh）
- 3.shell环境执行：在当前的shell环境中执行（使用 . + 脚本 或 source + 脚本）
- 4.区别：前两种会使用一个新的bash子进程来执行
![image](https://github.com/NightBonsai/Linux_README/assets/107353989/fa190b8d-47e4-4d0f-8d93-bdd9feb68085)<br>
![image](https://github.com/NightBonsai/Linux_README/assets/107353989/91fdddad-0a51-4eb5-8254-4bdc0d10a9d5)<br>

### 指令定位：
- 问题：一般终端的输入指令执行都是绝对路径执行，常规命令无需输入命令脚本路径
- 原因：常用指令可执行文件直接打包在某些特定位置，这些位置写入了全局变量。bash执行不知道位置的指令时就会搜索全局变量PATH中所包含的路径
