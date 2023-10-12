# Linux_README

## 目录
[返回主目录](https://github.com/NightBonsai/Linux_README/blob/main/README.md)

## Linux编译工具

### Linux编译工具：
- gcc（编译C）& g++（编译C++）

      gcc -E源文件-o文件名.i	预处理文件
      gcc -S文件名.i-o文件名.s	汇编文件
      gcc -C文件名.s-o文件名	可执行文件

      也可一步到位：gcc源文件-o文件名

### 动态链接库dll (Dynamic Link Library)：
- 把一些经常会共享的代码（静态链接的OBJ程序库）制作成DLL档
- 当可执行文件调用到DLL档内的函数时，Windows操作系统才会把DLL档加载存储器内

### Linux生成动态链接库（公用化，方便今后重新调用）：

    g++源文件名cpp -shared -fpic -o lib源文件名.so		
    -shared和-fpic要空格分开
    动态链接库移动至/usr/lib/
    使用动态链接库
    g++ main.cpp -o libmain -l源文件名（不需要文件后缀）

### Linux gdb代码调试工具：
1.生成可执行文件		-g

    gcc *.c -g -o	可执行文件

2.gdb ./可执行文件	进入调试模式

    l (list)：       查看代码
    r (run)：        运行
    b n (break n)：  在n行打断点
    c (continue)：   执行到下一个断点
    n (next)：       下一步
    watch变量名：     观察变量

### Linux make工具:
- 1.make自动推导:<br>

      make工具通过一个称为makefile的文件来完成并自动维护编译工作
      只要make看到一 个[.o]文件,它就会自动的把[.c]文件加在依赖关系中

- 2.makefile格式:

      目标文件：依赖文件
      命令
      目标文件1：依赖文件1
      命令
      clear：
      rm -f目标文件 目标文件1...

- 3.makefile最终版：

      ELF=最终要生成的目标文件名
      src=$(wildcard *.cpp) 	//wildcard函数: 当前目录下匹配模式的文件
      object=$(src: .cpp=.o) 	//src..cpp=.o：模式匹配替换

      $(ELF) : $(object)
      g++ $(object) -o $@ /$@：规则的目标文件名
      $(object) :
      clean:
      rm -f $(object) $(ELF)

- 4.自动编译make
- 5.删除目标文件make clear

### Makefile工作原理：

    make会在当前目录下找名字叫makefile的文件
    如果找到，它会找文件中的第一个目标文件，并且把这个文件作为最终的目标文件
    如果该文件不存在，或是其所依赖的后面的.o文件的文件修改时间要比其新，它就会执行后面所定义的命令来生成新的第一个目标文件
    如果第一个目标文件所依赖的**.o文件也存在**，那么make会在当前文件中找目标为.o文件的依赖性，根据之前的新旧或是否存在的规则，来生成新的.o文件
