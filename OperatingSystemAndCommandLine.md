

[TOC]

注：仅用于个人学习

# 1 Linux

## 1.1 常用命令

### 1.1.1 系统命令

#### 1.1.1.1 环境变量实时生效

功能：使得新建立的环境变量立刻生效，而不用重新启动系统。

```bash
source /etc/profile
```

/etc/profile文件的改变会涉及到系统的环境，也就是有关Linux环境变量的文件。

使用env命令显示所有的环境变量 。在命令提示符下键入env就行了。

set命令显示所有本地定义的Shell变量。

常见的环境变量：

PATH：决定了shell将到哪些目录中寻找命令或程序

HOME：当前用户主目录

MAIL：是指当前用户的邮件存放目录。

SHELL：是指当前用户用的是哪种Shell。

HISTSIZE：是指保存历史命令记录的条数。

LOGNAME：是指当前用户的登录名。

HOSTNAME：是指主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的。

LANG/LANGUGE：是和语言相关的环境变量，使用多种语言的用户可以修改此环境变量。

PS1：是基本提示符，对于root用户是#，对于普通用户是$。

PS2：是附属提示符，默认是“>”。可以通过修改此环境变量来修改当前的命令符，比如下列命令会将提示符修改成字符串“Hello,My NewPrompt :) ”。

PS1=” Hello,My NewPrompt :) “

使用修改.bashrc文件（在用户的家目录下）进行环境变量的编辑，只对当前用户有用。使用修改 /etc/profile 文件进行环境变量的编辑，是对所有用户有用。大家一定要注意区别。

Linux profile文件在系统启动时将被运行。大家可以在里面加入其他命令，但是一定要加正确，不然的话系统会启动不起来的。

#### 1.1.1.2 修改环境变量

如何添加环境变量。

例如添加”NAME=liheng“ 。在profile文件的最后添加如下内容**export** NAME=liheng

变量值liheng可以加引号也可以不加，效果一样。

1、在终端输入$sudo gedit /etc/profile，打开profile文件，profile是系统级的环境

```bash
sudo gedit /etc/profile
```

2、在文件末尾添加一行：

export  PATH=/home/grant/anaconda2/bin:$PATH，其中，将“/home/grant/anaconda2/bin”替换为你实际的安装路径，保存。

3、使环境变量生效
方法1：
让/etc/profile文件修改后立即生效 ,可以使用如下命令:

```bash
.  /etc/profile
```

注意: . 和 /etc/profile 有空格
方法2：
让/etc/profile文件修改后立即生效 ,可以使用如下命令:

```bash
source /etc/profile
```

#### 1.1.1.3 查看Ubuntu系统版本

查看当前Ubuntu系统的版本

```bash
uname -a 
```

### 1.1.2 工具命令

#### 1.1.2.1 查看cuda版本

ubuntu: 查看cuda版本

```bash
nvcc -V
```

或者

```bash
cat /usr/local/cuda/version.txt
```

cudnn 版本

```
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```

## 1.2 MakeFile（服务器、开发板）

### 1.2.1 make makefile cmake qmake区别

1. gcc是GNU Compiler Collection（就是GNU编译器套件），也可以简单认为是编译器，它可以编译很多种编程语言（括C、C++、Objective-C、Fortran、Java等等）。

   编译器套件

2. 当你的程序只有一个源文件时，直接就可以用gcc命令编译它。

3. 但是当你的程序包含很多个源文件时，用gcc命令逐个去编译时，你就很容易混乱而且工作量大。

4. 所以出现了make工具
   make工具可以看成是一个智能的批处理工具，它本身并没有编译和链接的功能，而是用类似于批处理的方式：通过调用makefile文件中用户指定的命令来进行编译和链接的。

   工具

5. makefile是什么？简单的说就像一首歌的乐谱，make工具就像指挥家，指挥家根据乐谱指挥整个乐团怎么样演奏，make工具就根据makefile中的命令进行编译和链接的。

6. makefile命令中就包含了调用gcc（也可以是别的编译器）去编译某个源文件的命令。

7. makefile在一些简单的工程完全可以人工手下，但是当工程非常大的时候，手写makefile也是非常麻烦的，如果换了个平台makefile又要重新修改。

8. 这时候就出现了Cmake这个工具，cmake就可以更加简单的生成makefile文件给上面那个make用。当然cmake还有其他功能，就是可以跨平台生成对应平台能用的makefile，你不用再自己去修改了。

   项目管理工具

9. 可是cmake根据什么生成makefile呢？它又要根据一个叫CMakeLists.txt文件（学名：`组态档`）去生成makefile。

10. 到最后CMakeLists.txt文件谁写啊？亲，是你自己手写的。

11. 当然如果你用IDE，类似VS这些一般它都能帮你弄好了，你只需要按一下那个三角形。

12. 接着是qmake，qmake是什么，先说一下Qt这个东西。

    Qt是跨平台C++图形用户界面应用程序开发框架。它既可以开发GUI程序，也可用于开发非GUI程序，比如控制台工具和服务器。

    简单的说就是C++的第三方库，使用这个库你可以很容易生成windows，Linux，MAC os等等平台的图形界面。现在的Qt还包含了开发各种软件一般需要用到的功能模块（网络，数据库，XML，多线程啊等等），比你直接用C++（只带标准内裤那种）要方便和简单。

    Qt专用项目管理工具

13. 你可以用Qt简简单单就实现非常复杂的功能，是因为Qt对C++进行了扩展，你写一行代码，Qt在背后帮你写了几百上千行，而这些多出来的代码就是靠Qt专有的moc编译器（The Meta-Object Compiler）和uic编译器（User Interface Complier）来重新翻译你那一行代码。

    问题来了，你在进行程序编译前就必须先调用moc和uic对Qt源文件进行预处理，然后再调用编译器进行编译。上面说的那种普通makefile文件是不适用的，它没办法对qt源文件进行预处理。所以qmake就产生了。

14. qmake工具就是Qt公司制造出来，用来生成Qt 专用makefile文件，这种makefile文件就能自动智能调用moc和uic对源程序进行预处理和编译。qmake当然必须也是跨平台的，跟cmake一样能对应各种平台生成对应makefile文件。

15. qmake是根据Qt 工程文件（.pro）来生成对应的makefile的。工程文件（.pro）相对来说比较简单，一般工程你都可以自己手写，但是一般都是由Qt的开发环境 Qt Creator自动生成的，你还是只需要按下那个邪恶三角形就完事了。

    .pro

16. 还没有完，由于qmake很简单很好用又支持跨平台，而且是可以独立于它的IDE，所以你也可以用在非Qt工程上面，照样可以生成普通的makefile，只要在pro文件中加入CONFIG -= qt  就可以了。

17. 这样qmake和cmake有什么区别？不好意思，cmake也是同样支持Qt程序的，cmake也能生成针对qt 程序的那种特殊makefile，只是cmake的CMakeLists.txt 写起来相对与qmake的pro文件复杂点。

    qmake 是为 Qt 量身打造的，使用起来非常方便，但是cmake功能比qmake强大。 一般的Qt工程你就直接使用qmake就可以了，cmake的强大功能一般人是用不到的。

    当你的工程非常大的时候，又有qt部分的子工程，又有其他语言的部分子工程，据说用cmake会方便，我也没试过。

### 1.2.2 makefile

Makefile文件为：

```text
VERSION = 1.0.0     #程序版本号  

SOURCE = $(wildcard ./src/*.c)  #获取所有的.c文件  
OBJ = $(patsubst %.c, %.o, $(SOURCE))   #将.c文件转为.o文件  
INCLUDES = -I./h    #头文件路径  

LIBS = -ldylib      #库文件名字  
LIB_PATH = -L./lib  #库文件地址  

DEBUG = -D_MACRO    #宏定义  
CFLAGS = -Wall -c   #编译标志位  

TARGET = app  
CC = gcc  

$(TARGET): $(OBJ)     
    @mkdir -p output/   #创建一个目录，用于存放已编译的目标  
    $(CC) $(OBJ) $(LIB_PATH) $(LIBS) -o output/$(TARGET).$(VERSION)  

%.o: %.c  
    $(CC) $(INCLUDES) $(DEBUG) $(CFLAGS) $< -o $@  

.PHONY: clean  
clean:  
    rm -rf $(OBJ) output/   
```

库文件说明：

库文件名称为libdylib.so，里面只有一个函数：dynamic_lib_call()，它就输出一句话：this is a function in dynamic library。

**3. Makefile所包含内容**

**3.1 程序版本**

软件开发过程中，会产生多个版本程序，通常会在程序末尾加上版本号后缀。

```text
VERSION = 1.0.0 #定义  
$(CC) $(OBJ) $(LIB_PATH) $(LIBS) -o output/$(TARGET).$(VERSION) #使用  
```

**3.2 头文件**

由于.c文件与.h文件分开在不同目录下，所以应指定头文件路径。

```text
INCLUDES = -I./h   
```

**3.3 宏定义**

在代码调试的过程中，我们通常会加个宏定义来控制此段代码是否被编译，比如：

```text
#ifdef _MACRO  
    printf("macro test\n");  
#endif  
```

具体的宏我们可不定义在代码里，可在Makefile里指定，比如：

```text
DEBUG = -D_MACRO    #定义  
$(CC) $(INCLUDES) $(DEBUG) $(CFLAGS) $< -o $@    #使用  
```

**3.4 编译选项**

当编译选项较多时，我们通常会把它单独拿出来，比如：

```text
CFLAGS = -Wall -c       #定义  
$(CC) $(INCLUDES) $(DEBUG) $(CFLAGS) $< -o $@    #使用  
```

**3.5 库**

代码里如果要使用到库，我们可以将库名字和路径分别拿出来，比如：

```text
LIBS = -ldylib          #库文件名字  
LIB_PATH = -L./lib      #库文件地址  
$(CC) $(OBJ) $(LIB_PATH) $(LIBS) -o output/$(TARGET).$(VERSION) #使用  
```

**3.6 output目录**

如果不想把生成的程序与源文件混在一起，可将生成的程序单独放在一个output目录，比如：

```text
$(TARGET): $(OBJ)  
        @mkdir -p output/       #创建一个目录，用于存放已编译的目标  
        $(CC) $(OBJ) $(LIB_PATH) $(LIBS) -o output/$(TARGET).$(VERSION)  
```

**4. 编译执行结果**

<img src="https://pic1.zhimg.com/50/v2-a8d0ba77d79eae5b09b88f77631dc784_hd.jpg" data-caption="" data-size="normal" data-rawwidth="874" data-rawheight="182" data-default-watermark-src="https://pic2.zhimg.com/50/v2-1c2bd5b38b2637f3a394510f6810eb1c_hd.jpg" class="origin_image zh-lightbox-thumb" width="874" data-original="https://pic1.zhimg.com/v2-a8d0ba77d79eae5b09b88f77631dc784_r.jpg"/>



### 1.2.3 CMake 

cmake打包







https://zhuanlan.zhihu.com/p/33562243





### 1.2.4 .a和.so （`程序员的自我修养`得好好看看）

喜欢用静态库的一个主要原因是因为懒，因为静态库什么都不用设置。
静态库面临这么多重大问题，居然没有人提。
1、如果静态库中有全局变量，那么在几个模块中使用，将会导致全局变量有不同的值，这是非常严重的问题。
2、静态库编译时，不会进行链接检查，所以这么多静态库的问题，在生成静态库阶段检查不出来。
3、几个模块，引用同一静态库，如果有一模块没有编译到，会引起巨大的差异导致问题。
动态库最大的好处是什么，不仅仅是代码共享，更重要的是“模块化”。



#### 1.2.4.1 原理

```text
什么是库？
```

库是写好的现有的，成熟的，可以复用的代码。**现实中每个程序都要依赖很多基础的底层库，不可能每个人的代码都从零开始，因此库的存在意义非同寻常**。

本质上来说库是一种可执行代码的二进制形式，可以被操作系统载入内存执行。**库有两种：静态库（****.a、.lib）和动态库（.so、.dll）。  windows上对应的是.lib .dll linux上对应的是.a .so**

在这里先介绍下Linux下的gcc编译的几个选项

```text
g++ -c hellospeak.cpp
```

会将hellospeak.cpp  选项 -c 用来告诉编译器编译源代码但不要执行链接，输出结果为对象文件。文件默认名与源码文件名相同，只是将其后缀变为 .o。例如，上面的命令将编译源码文件hellospeak.cpp 并生成对象文件 hellospeak.o；

下面这条命令将上述两个源码文件编译链接成一个单一的可执行程序： 

```text
$ g++ hellospeak.cpp speak.cpp -o hellospeak
```

如果没有-o和后面的参数，编译器采用默认的 a.out

本例中就会生成hellospeak 这样的可执行程序

所谓静态、动态是指链接。回顾一下，将一个程序编译成可执行程序的步骤：

图：编译过程

<img src="https://pic2.zhimg.com/50/72b693726d70eea37aacbb93d8d40a43_hd.jpg" data-rawwidth="554" data-rawheight="263" class="origin_image zh-lightbox-thumb" width="554" data-original="https://pic2.zhimg.com/72b693726d70eea37aacbb93d8d40a43_r.jpg"/>

静态库

之所以成为【静态库】，**是因为在链接阶段，会将汇编生成的目标文件****.o与引用到的库一起链接打包到可执行文件中。因此对应的链接方式称为静态链接。**

试想一下，静态库与汇编生成的目标文件一起链接为可执行文件，**那么静态库必定跟****.o****文件格式相似**。其实一个静态库可以简单看成是**一组目标文件（****.o/.obj****文件）的集合**，即很多目标文件经过压缩打包后形成的一个文件。静态库特点总结：

**l  静态库对函数库的链接是放在编译时期完成的。**

**l  程序在运行时与函数库再无瓜葛，移植方便。**

**l  浪费空间和资源，因为所有相关的目标文件与牵涉到的函数库被链接合成一个可执行文件。**

Linux下创建与使用静态库

Linux静态库命名规则

Linux静态库命名规范，必须是"lib[your_library_name].a"：lib为前缀，中间是静态库名，扩展名为.a。

创建静态库（.a）

通过上面的流程可以知道，Linux创建静态库过程如下：

l  首先，将代码文件编译成目标文件.o（StaticMath.o）

**g++ -c StaticMath.cpp**

注意带参数-c，否则直接编译为可执行文件

l  然后，通过ar工具将目标文件打包成.a静态库文件

**ar -crv libstaticmath.a StaticMath.o**

生成静态库**libstaticmath****.a**。

<img src="https://pic1.zhimg.com/50/f798fdffbee291d83ad26a08ed1b28ac_hd.jpg" data-rawwidth="554" data-rawheight="180" class="origin_image zh-lightbox-thumb" width="554" data-original="https://pic1.zhimg.com/f798fdffbee291d83ad26a08ed1b28ac_r.jpg"/>

-------------------------------分割线------------------------

动态库

通过上面的介绍发现静态库，容易使用和理解，也达到了代码复用的目的，那为什么还需要动态库呢？

为什么还需要动态库？

为什么需要动态库，其实也是静态库的特点导致。

l  空间浪费是静态库的一个问题。

<img src="https://pic2.zhimg.com/50/6aac2e2dc8faa8d1008f5320a7a83f5d_hd.jpg" data-rawwidth="483" data-rawheight="413" class="origin_image zh-lightbox-thumb" width="483" data-original="https://pic2.zhimg.com/6aac2e2dc8faa8d1008f5320a7a83f5d_r.jpg"/>

另一个问题是静态库对程序的更新、部署和发布页会带来麻烦。如果静态库liba.lib更新了，所以使用它的应用程序都需要重新编译、发布给用户（对于玩家来说，可能是一个很小的改动，却导致整个程序重新下载，**全量更新**）。

动态库在程序编译时并不会被连接到目标代码中，而是在程序运行是才被载入。**不同的应用程序如果调用相同的库，那么在内存里只需要有一份该共享库的实例**，规避了空间浪费问题。动态库在程序运行是才被载入，也解决了静态库对程序的更新、部署和发布页会带来麻烦。用户只需要更新动态库即可，**增量更新**。

<img src="https://pic3.zhimg.com/50/73f097608fecb37ffc4128273341376e_hd.jpg" data-rawwidth="459" data-rawheight="404" class="origin_image zh-lightbox-thumb" width="459" data-original="https://pic3.zhimg.com/73f097608fecb37ffc4128273341376e_r.jpg"/>

动态库特点总结：

l  动态库把对一些库函数的链接载入推迟到程序运行的时期。

l  可以实现进程之间的资源共享。（因此动态库也称为共享库）

l  将一些程序升级变得简单。

l  甚至可以真正做到链接载入完全由程序员在程序代码中控制（**显示调用**）。

Window与Linux执行文件格式不同，在创建动态库的时候有一些差异。

l  在Windows系统下的执行文件格式是PE格式，动态库需要一个**DllMain**函数做出初始化的入口，通常在导出函数的声明时需要有_declspec(dllexport)**关键字**。

l  Linux下gcc编译的执行文件默认是ELF格式，**不需要初始化入口，亦不需要函数做特别的声明，**编写比较方便。

与创建静态库不同的是，不需要打包工具（ar、lib.exe），直接使用编译器即可创建动态库。



### 1.2.5 GDB

## **1.GDB 相关概念**

GDB, 是 The GNU Project Debugger 的缩写, 是 Linux 下功能全面的调试工具。GDB 支持断点、单步执行、打印变量、观察变量、查看寄存器、查看堆栈等调试手段。在 Linux 环境软件开发中，GDB 是主要的调试工具，用来调试 C 和 C++ 程序。

## **2.GDB 的进入和退出**

如果要调试程序，需要在 gcc 编译可执行程序时加上 -g 参数，首先我们编译 bugging.c 程序，生成可执行文件：

```text
gcc -g -o bugging bugging.c
```

其中 -o 指定输出文件名, 实验楼的环境是 64 位的 Ubuntu 14.04，所以默认会编译为 64 位的程序。

输入 gdb bugging 进入 gdb 调试 bugging 程序的界面：

```text
gdb bugging
```

在 gdb 命令行界面，输入run 执行待调试程序：

```text
(gdb) run
```

在 gdb 命令行界面，输入quit 退出 gdb：

```text
(gdb) quit
```

上述步骤的操作截图如下：

![img](assets/v2-97fd94455a982960e454f7d5a887f255_hd.jpg)

## **3.GDB 命令行界面使用技巧**

## **命令补全**

任何时候都可以使用 TAB 进行补全，如果只有一个待选选项则直接补全；否则会列出可选选项，继续键入命令，同时结合 TAB 即可快速输入命令。

## **部分 gdb 常用命令一览表**

**命令简写形式说明**listl查看源码backtracebt、where打印函数栈信息nextn执行下一行steps一次执行一行，遇到函数会进入finish运行到函数结束continuec继续运行breakb设置断点info breakpoints显示断点信息deleted删除断点printp打印表达式的值runr启动程序untilu执行到指定行infoi显示信息helph帮助信息

## **查询用法**

在 gdb 命令行界面，使用 (gdb) help command 可以查看命令的用法。

## **执行 Shell 命令**

在 gdb 命令行界面可以执行外部的 Shell 命令：

```text
(gdb) !shell 命令
```

例如查看当前目录的文件：

![img](assets/v2-c08a0098a0308dc8e91b5be95adad6f7_hd.jpg)

## **二、GDB 断点**

## **1.重新进入 debugging 调试界面**

```text
gdb bugging
```

## **2.查看源码**

*list* 命令用来显示源文件中的代码。

## **通过行号查看源码**

list 行号，显示某一行附近的代码：

![img](assets/v2-cfd983739a622d3933b2a8924f85fde2_hd.png)

list 文件名 : 行号，显示某一个文件某一行附近的代码，用于多个源文件的情况。

## **通过函数查看源码**

list 函数名，显示某个函数附近的代码：

![img](assets/v2-efee1d5dd29f547ce2702a57489266bd_hd.png)

list 文件名 : 函数名，显示某一个文件某个函数附近的代码，用于多个源文件的情况。

## **3 设置断点**

*break* 命令用来设置断点。

## **通过行号设置断点**

break 行号，断点设置在该行开始处，**注意：该行代码未被执行**：

![img](assets/v2-cbf30eb9d44b22657d2dc29001af516a_hd.png)

break 文件名 : 行号，适用于有多个源文件的情况。

## **通过函数设置断点**

break 函数名，断点设置在该函数的开始处，**断点所在行未被执行**：

![img](assets/v2-cf12626b4f41022b7ee99a515311de17_hd.png)

break 文件名 : 函数名，适用于有多个源文件的情况。

## **4 查看断点信息**

*info breakpoints* 命令用于显示当前断点信息。

![img](assets/v2-315b1ecf67eb0057124fab767cc25dca_hd.png)

其中每一项的信息：

- Num 列代表断点编号，该编号可以作为 delete/enalbe/disable 等控制断点命令的参数
- Type 列代表断点类型，一般为 breakpoint
- Disp 列代表断点被命中后，该断点保留(keep)、删除(del)还是关闭(dis)
- Enb 列代表该断点是 enable(y) 还是 disable(n)
- Address 列代表该断点处虚拟内存的地址
- What 列代表该断点在源文件中的信息

## **5 删除断点**

*delete* 命令用于删除断点。

## **删除指定断点**

delete Num，删除指定断点，断点编号可通过 info breakpoints 获得：

![img](assets/v2-45f028467c6bfeeee45aae11e4549a89_hd.png)

## **删除所有断点**

delete，不带任何参数，默认删除所有断点。

## **6 关闭和启用断点**

*disable* 命令用于关闭断点，有些断点可能暂时不需要但又不想删除，便可以 disable 该断点。

*enable* 命令用于启用断点。

## **关闭所有断点**

disable，不带任何参数，默认关闭所有断点。

## **关闭指定断点**

disable Num，关闭指定断点，断点编号可通过 info breakpoints 获得：

![img](assets/v2-c85d8a8e3a39a1e359f3c1dd17daf718_hd.png)

## **启用所有断点**

enable，不带任何参数，默认启用所有断点。

## **启用指定断点**

enable Num，启用指定断点，断点编号可通过 info breakpoints 获得。

![img](assets/v2-d0206945706acbaf5f97fd7791fd1bfa_hd.png)

**disable 和 enable 命令影响的是 info breakpoints 的 Enb 列，表示该断点是启用还是关闭**

## **7 断点启用的更多方式**

*enable* 命令还可以用来设置断点被执行的次数，比如当断点设在循环中的时候，某断点可能多次被命中。

## **断点 hit 一次之后关闭该断点**

```text
enable once Num
```

## **断点 hit 一次之后删除该断点**

```text
enable delete Num
```

实验中我们可以如下图测试该功能：

![img](assets/v2-c86c83b5af0c13c30054fd5e72fe7daf_hd.png)

**这两个命令影响的是 info breakpoints 的 Disp 列，表示该断点被命中之后的行为**

## **8 断点小结**

断点是调试最基本的方法之一，这一节主要介绍了断点相关的知识。主要是几个断点相关的命令。

- list
- info breakpoints
- break
- delete
- disable 和 enable
- enable once 和 enable delete

不熟悉命令的时候，记得在 gdb 命令行下键入 help info breakpoints 等命令，查询帮助文档。



## **最后**

文章所有内容均截选自实验楼教程[【GDB 简明教程】](https://link.zhihu.com/?target=https%3A//www.shiyanlou.com/courses/496)，教程还介绍了以下内容：

- GDB 单步调试；
- GDB 函数栈；
- 对有问题的链表程序的调试来逐步实践挖掘程序 BUG 的过程；



常用命令：

1、打开GDB：gdb

2、打开要调试的文件：file xxx

设置参数：set args xxx xxx

显示缺省的参数列表：show args

3、在某处（第几行）下断点：break x

删除N号断点：delete N

*删除所有断点： delete

4、单步调试，步入当前函数：s

5、单步调试，步过当前函数：n

6、打印xxx的内容：print xxx

7、执行到当前函数返回：finish

执行完当前的循环：until

8、打印当前栈帧的本地变量：info locals

9、反汇编一个函数：disassemble xxx

10、查看当前运行的文件和行：backtrace

11、继续运行程序直接运行到下一个断点：continue

#### 1.2.5.2 PDB

如果你还主要靠print来调试代码，那值得花10分钟试试pdb这个Python自带的Debug工具。

pdb有2种用法：

- **非侵入式方法**（不用额外修改源代码，在命令行下直接运行就能调试）

```bash
python3 -m pdb filename.py
```

- **侵入式方法**（需要在被调试的代码中添加一行代码然后再正常运行代码）

```python3
import pdb;pdb.set_trace()
```

当你在命令行看到下面这个提示符时，说明已经正确打开了pdb

```text
(Pdb) 
```

然后就可以开始输入pdb命令了，下面是pdb的常用命令

## 1、查看源代码

命令：

```text
l
```

说明：

> 查看当前位置前后11行源代码（多次会翻页）
> 当前位置在代码中会用-->这个符号标出来



命令：

```text
ll
```

说明：

> 查看当前函数或框架的所有源代码

## 2、添加断点

命令：

```text
b
b lineno
b filename:lineno 
b functionname
```

参数：

> filename文件名，断点添加到哪个文件，[如test.py](https://link.zhihu.com/?target=http%3A//xn--test-f96g.py/)
> lineno断点添加到哪一行
> function：函数名，在该函数执行的第一行设置断点

说明：

> 1.不带参数表示查看断点设置
> 2.带参则在指定位置设置一个断点

## 3、添加临时断点

命令：

```text
tbreak
tbreak lineno
tbreak filename:lineno
tbreak functionname
```

参数：

> 同b

说明：

> 执行一次后时自动删除（这就是它被称为临时断点的原因）

## 4、清除断点

命令：

```pycon
cl
cl filename:lineno
cl bpnumber [bpnumber ...]
```

参数：

> bpnumber 断点序号（多个以空格分隔）

说明：

> 1.不带参数用于清除所有断点，会提示确认（包括临时断点）
> 2.带参数则清除指定文件行或当前文件指定序号的断点

## 5、打印变量值

命令：

```text
p expression
```

参数：

> expression Python表达式

## 6、逐行调试命令

包括 s ，n ， r 这3个相似的命令，区别在如何对待函数上

命令1：

```text
s
```

说明：

> 执行下一行（能够进入函数体）



命令2：

```text
n 
```

说明：

> 执行下一行（不会进入函数体）



命令3：

```text
r 
```

说明：

> 执行下一行（在函数中时会直接执行到函数返回处）

## 7、非逐行调试命令

命令1：

```text
c 
```

说明：

> 持续执行下去，直到遇到一个断点



命令2

```text
unt lineno
```

说明：

> 持续执行直到运行到指定行（或遇到断点）



命令3

```text
j lineno
```

说明：

> 直接跳转到指定行（注意，被跳过的代码不执行）

## 8、查看函数参数

命令：

```text
a
```

说明：

> 在函数中时打印函数的参数和参数的值



## 9、打印变量类型

命令：

```text
whatis expression
```

说明：

> 打印表达式的类型，常用来打印变量值

## 10、启动交互式解释器

```text
interact
```

说明：

> 启动一个python的交互式解释器，使用当前代码的全局命名空间（使用ctrl+d返回pdb）

## 11、打印堆栈信息

```text
w
```

说明：

> 打印堆栈信息，最新的帧在最底部。箭头表示当前帧。

## 12、退出pdb

```text
q
```



完成了。好吧，可能超过了10分钟，我承认这是一个善意的谎言，不过至此你已经掌握了，击个掌吧。

## 1.3 ARM（区别于服务器）

### 1.3.1 Cortex-A76（差不多能做到i5-5200水平）

处理器

型号: HUAWEI Kirin 980 （麒麟980）

核数: 八核

主频: 2*Cortex-`A76` Based 2.6GHz+ 2*Cortex-`A76` Based 1.92GHz+ 4*Cortex-`A55` 1.8GHz

GPU: Mali G76 720MHz

NPU: 双NPU(神经网络处理单元)

#### 1.3.1.1 性能对比

具体来说，大家喜闻乐见的骁龙845 CPU部分就是基于ARM Cortex-A75和A55架构“改修”而来，上代的骁龙835 CPU本质上是ARM Cortex-A73的“变体”；而华为麒麟960、970等，更是原封不动地买来了公版的ARM CPU和GPU设计，就算是这三家中“原创度”最高的三星，旗舰芯片Exynos 9810的大核心是自己原创的，但是小核心也是ARM的公版Cortex-A55无误。

对于Cortex-A76的性能，ARM官方资料提供了对比数据：Cortex-A76相比于“上上代”的Cortex-A73，整数性能提升了90%，浮点性能提升了150%，而综合起来的性能增幅也有80%。如果是和上一代的Cortex-A75相比，那么综合性能提升幅度也高达35%。

同时，ARM还说，由于指令集层面上的改进，Cortex-A76运行“机器学习应用”时的性能最高可以提升400%，而在能效比上，新架构也有着高达40%的改进……

#### 1.3.1.2 主频提升换来的性能涨幅（7nm-3GHz-5W）

是不是觉得“很好很强大”，别急，让我们来做个简单的算术：

在ARM的官方对比资料中，最新款的Cortex-A76测试平台使用了目前尚未量产的7nm制程，运行在3GHz频率下；而惨遭秒杀的“前前代”Cortex-A73则是基于现有的10nm制程，主频仅有2.45GHz，同样被拿来对比的Cortex-A75主频也是只跑到了2.8GHz——换言之，所谓“80%的性能提升”，其实并非同频率下测得，并不能完全反应架构革新带来的执行效率增加。

因此，假设官方资料中的Cortex-A73性能指标为100（参考值），则可以算出，在相同频率下，全新的A76架构同频性能相比两代之前的A73，实际的提升程度是(180/3)/（100/2.45)-100%=47.02%；而如果和当下的A75架构相比，则实际同频性能提升则仅有（180/3)/(145/2.8)-100%=15.9%……

一言以蔽之：只考虑架构上的改变的话，全新的Cortex-A76其实并没有比现有的Cortex-A75强很多。

#### 1.3.1.3 i7-7700也靠提频（4.2-4.5GHZ-91W）

同频性能不提升的情况下，直接拉升新处理器的主频，的确也是一种行之有效的性能提升办法。

这方面典型的例子就是台式电脑上的英特尔酷睿i7 7700K与6700K之间的提升——英特尔自家都承认，7700K的同频性能相比6700K完全没变化。但是靠着高了10%的主频，7700K的实际性能就是比6700K高了10%。

#### 1.3.1.4 绝大时间达不到主频

在手机上，不管是多“旗舰”的SoC芯片，其在工作的绝大部分时间里都根本达不到标称的最高主频——2.8GHz的骁龙845，即便是在运行3DMARK这样的高负载跑分软件时，最高也只有2.3GHz的主频记录。

更不要说3GHz的“Cortex-A76”了，就算用上了7nm制程，其真正在手机里，也绝不可能一直运行在3GHz下。换句话说，当这种性能“打折扣”的时候，它的实际体验会不会比前代旗舰们有明显的差异，其实就很难说了。

#### 1.3.1.5 绝大时间达不到主频

A11确实是基于ARM构架改动的，三星的9810也是一样，只不过这2家动手能力强点。

### 1.3.2 ARM家族

所谓处理器架构是CPU厂商给属于同一系列的CPU产品定的一个规范，主要目的是为了区分不同类型CPU的重要标示。目前市面上的CPU指令集分类主要分有两大阵营，一个是intel、AMD为首的复杂指令集CPU，另一个是以IBM、ARM为首的精简指令集CPU。不同品牌的CPU，其产品的架构也不相同。例如，Intel、AMD的CPU是X86架构的，而IBM公司的CPU是PowerPC架构，ARM公司是ARM架构。

![ARM Cortex-Aç³»åå¤çå¨æ§è½å·®å¼å¯¹æ¯](assets/1472460435291167.png!0)

​		如图所示，绿色的部分都是v7-A的架构，蓝色的是v8-A架构，基本上绿色都是可以支持到32和64位的，除了A32，只支持到32位。在右边的每个部分，比如说需要高效能的最上面的A15-A73这个部分是最高效的，接下来就是比较注重整个效率的部分了，中间那个部分是比较高效率的，最下面那栏的是效率最好的，在电池的效能方面达到了最好的标准。

　　如果非要给他们一个排序的话，从高到低大体上可排序为：Cortex-A73处理器、Cortex-A72处理器、Cortex-A57处理器、Cortex-A53处理器、Cortex-A35处理器、Cortex-A32处理器、Cortex-A17处理器、Cortex-A15处理器、Cortex-A7处理器、Cortex-A9处理器、Cortex-A8处理器、Cortex-A5处理器。

![ARM Cortex-A系列处理器性能差异对比](assets/1472539838631177.jpg!0)

 

| 架构  | 处理器家族                                                   |
| :---- | :----------------------------------------------------------- |
| ARMv1 | [ARM1](http://zh.wikipedia.org/w/index.php?title=ARM1&action=edit&redlink=1) |
| ARMv2 | [ARM2](http://zh.wikipedia.org/w/index.php?title=ARM2&action=edit&redlink=1)、[ARM3](http://zh.wikipedia.org/w/index.php?title=ARM3&action=edit&redlink=1) |
| ARMv3 | ARM6, [ARM7](http://zh.wikipedia.org/wiki/ARM7)              |
| ARMv4 | [StrongARM](http://zh.wikipedia.org/wiki/StrongARM)、[ARM7TDMI](http://zh.wikipedia.org/wiki/ARM7TDMI)、[ARM9](http://zh.wikipedia.org/wiki/ARM9)TDMI |
| ARMv5 | [ARM7EJ](http://zh.wikipedia.org/w/index.php?title=ARM7EJ&action=edit&redlink=1)、[ARM9E](http://zh.wikipedia.org/w/index.php?title=ARM9E&action=edit&redlink=1)、[ARM10E](http://zh.wikipedia.org/w/index.php?title=ARM10E&action=edit&redlink=1)、[XScale](http://zh.wikipedia.org/wiki/XScale) |
| ARMv6 | [ARM11](http://zh.wikipedia.org/w/index.php?title=ARM11&action=edit&redlink=1)、[ARM Cortex-M](http://zh.wikipedia.org/w/index.php?title=ARM_Cortex-M&action=edit&redlink=1) |
| ARMv7 | [ARM Cortex-A](http://zh.wikipedia.org/w/index.php?title=ARM_Cortex-A&action=edit&redlink=1)、[ARM Cortex-M](http://zh.wikipedia.org/w/index.php?title=ARM_Cortex-M&action=edit&redlink=1)、[ARM Cortex-R](http://zh.wikipedia.org/w/index.php?title=ARM_Cortex-R&action=edit&redlink=1) |
| ARMv8 | Cortex-A50[[9\]](http://zh.wikipedia.org/wiki/ARM架構#cite_note-cortex-a50_announce-9) |



　



## 1.4 海思系列

### 1.4.1 Hi3559AV100（至少达到3个tx1的水平）

Hi3559AV100 硬件信息

CPU:

双核 ARM Cortex A73@1.8GHz，32KB I-Cache，64KB D-Cache /512KB L2 cache

双核 ARM Cortex A53@1.2GHz，32KB I-Cache，32KB D-Cache /256KB L2 cache

单核 ARM Cortex A53@1.2GHz，32KB I-Cache，32KB D-Cache /128KB L2 cache

支持 Neon 加速，集成 FPU 处理单元

GPU:

双核 ARM Mali G71@900MHz，256KB cache

支持 OpenCL 1.1/1.2/2.0

支持 OpenGL ES 3.0/3.1/3.2

智能视频分析：

提供视觉计算处理能力

四核 DSP@700MHz，32K I-Cache /32K IRAM/512KB DRAM

双核 NNIE@840MHz 神经网络加速引擎

内置双目深度检测单元



测试网络信息

googlenet 5ms

resnet50 10.5ms

vgg16 35ms

squeezenet 2.8ms

alexnet 9ms

#### 1.4.1.1

#### 1.4.1.2 其他

NNIE的问题，一共1024个MAC，常压频率840MHZ，双核，可以基于caffe直接编程

# 2 Windows

## 2.1 命令行

##  2.2 批处理





# 3 软件层（侧重协议、概念）

## 3.1 shell、bash 和 zsh 等词的真正含义

### 3.1.1 解释与编译

编程语言没有编译型和解释型的区别，只能说某个语言常见的执行方式为*编译成新代码执行*或*解释器解释执行*
编译器的输入是A语言的源代码，而输出是B语言；比如C++，被编译成汇编语言。
解释器的输入是A语言的源代码，它直接执行A语言；一般解释器的内部实现是一个编译器加一个虚拟机，编译器把输入语言编译成中间语言，虚拟机直接执行中间语言。

### 3.1.2 terminal

一个程序，是界面上打开的黑框框本身，比如 xterm、kvt 等。shell 运行于其中。

### 3.1.3 shell（解释器） 

shell 是一个命令行解释器，顾名思义就是机器外面的一层壳，用于人机交互，只要是人与电脑之间交互的接口，就可以称为 shell。表现为其作用是用户输入一条命令，shell 就立即解释执行一条。不局限于系统、语言等概念、操作方式和表现方式等。 比如我们平时在黑框框里输入命令，叫 command-line interface (CLI)；在屏幕上点点点，叫 graphical user interface (GUI)。

### 3.1.4 Interactive 和 Non-interactive

Interactive，如果你打开 terminal，在里面输入 bash 代码，回车得到输出，你就是在运行一个 Interactive shell，它的特征是可以让用户输入，然后直接把输出打到界面上；如果你运行一个包含了若干行的 shell 脚本，这些 shell 代码就运行在Non-interactive shell 中。

### 3.1.5 Login 和 Non-login

login shell 是指登录系统后所获得的顶层 shell，比如最常用的 ssh 登录，登录完后得到一个 login shell
如果已经登录了桌面电脑，打开 terminal 进入的 shell 就是 Non-login shell。

### 3.1.6 shell的两种：sh，bash

常见的 shell 解释器有 sh、bash这两种，其他的 ksh、csh 和 zsh 等是不常见的。Mac OS 中默认安装了以上所有类型，Windows 需要自行安装，Linux 更不用说了。就像上面说的，只要一门语言有解释器，就可以作为 shell 使用。比如Java 有第三方解释器 Jshell，PHP有 PHP Shell。如果你用过 windows，那你对 cmd 这个词一定不陌、生，它是 windows shell，官方名称叫做 command interpreter。

#### 3.1.6.1 bash

Bash 是最常见的 shell，Mac 中默认 shell 就是 bash。
bash官网描述了唤起 bash shell 时加载的不同文件：login shell 加载 **~/.bash_profile** ，而non-login shell 加载 **~/.bashrc** 。

#### 3.1.6.2 zsh（早上）

很多人的 mac 中会使用 zsh 而不是 bash，一大半是因为 oh-my-zsh 这个配置集，它兼容 bash，还有自动补全等好用的功能。zsh 的配置文件\~/.zshrc

### 3.1.7 配置 shell

如上所说，shell 在启动时都会去找配置文件，然后运行它。你安装的一些脚本，如果想让它能够全局运行，就需要在配置文件中设置路径。有过设置路径后还是不管用的经历吗？多半是因为把配置写在了错误的配置文件里。

应该在配置shell（最常见的是配置默认命令）之前，使用 **echo $SHELL**，确认自己现在用的是什么shell后，再去编辑对应的配置文件 



## 3.2 SSH

### 3.2.1 SSH介绍

#### 3.2.1.1 SSH（协议）

什么是ssh？ ssh是“Secure Shell”的简写，Secure Shell协议是国际互联网工程任务组（The Internet Engineering Task Force，简称 IETF）制定的一个标准。目的是为了创建一个工作在应用层和传输层基础上的安全协议。避免数据的的明文传输。

#### 3.2.1.2 OpenSSH（具体实现）

什么是OpenSSH？ 前边说了，ssh是网络协议，而OpenSSH就是其中的一个具体实现。OpenSSH是由OpenBSD管理的项目之一，不过Openssh是跨平台的，支持linux、unix*，甚至windows。 所以实际应用中，我们用到的ssh基本上都是Openssh。

OpenSSH有哪些功能？ Secure Shell 是一个通信协议，在这个协议之上可以实现很多种应用层协议。从OpenSSH官网来看，OpenSSH提供了以下几个应用：

1. ssh，登录远程服务器、在远程服务器上执行命令。
2. scp，在两台主机之间实现文件拷贝。 
3. sftp，基于openssh实现的类似ftp程序。

除此之外，OpenSSH还提供了几个命令行工具，用来方便进行ssh操作： 

1. ssh-add 
2. ssh-keysign 
3. ssh-keyscan 
4. ssh-keygen

### 3.2.2 安装OpenSSH

大部分linux发行版都默认包含了OpenSSH客户端和服务器端，一些linux桌面发行版没有安装openssh服务器端。 如果没有安装，我们可以通过linux发行版的软件包管理工具进行安装。简单来说就是： apt-get系列：

```bash
sudo apt-get install openssh openssh-server
```

yum系列：

```bash
sudo yum install openssh openssh-server
```

其他系列：自己百度下。 备注：openssh是客户端、openssh-server是服务器端。不同的发行版名称可能不同，需要自己确认一下。 安装完毕之后，系统中就应该会有ssh命令了。这个时候就可以使用ssh来进行远程主机的管理了。

### 3.2.3 配置和启动ssh服务

在使用之前我们需要对ssh服务进行配置，在大多数linux系统中，ssh服务的配置文件为：/etc/ssh/sshd_config 使用vim进行编辑：

```bash
vim  /etc/ssh/sshd_config
```

以下地方根据实际情况进行修改（yes为允许、no为禁止）：

```bash
PermitRootLogin yes  #是否允许root账户登录
PasswordAuthentication yes  #是否允许使用密码校验登录
RSAAuthentication yes  
PubkeyAuthentication yes  #是否允许使用key登录
```

然后使用系统服务管理命令启动服务，在大部分linux系统下，命令为：service 或者 systemctl 启动ssh服务命令：

```bash
~# service sshd restart
```

或者

```bash
~# systemctl  restart sshd
```

### 3.2.4 登录远程主机

命令格式为：ssh 用户名@远程主机的ip地址:远程主机端口 示例：

```bash
ssh  root@192.168.0.1:22
```

或者：

```bash
ssh -p 22 root@192.168.0.1
```

> 注：ssh默认端口为22，远程主机为默认端口时，可省略端口号。

执行上述命令之后，首次登陆会询问是否保存秘钥，输入yes即可。然后会提示输入密码，输入该用户对应的远程主机密码即可。

### 3.2.5 ssh免密码登录

配置使用key登录ssh服务器（ssh免密码登录）

使用key登录，需四个步骤：

#### 3.2.5.1 允许key登录

 修改ssh服务配置文件允许key登录：

```bash
~# vim /etc/ssh/sshd_config
```

找到PubkeyAuthentication这一行，改成：

```bash
PubkeyAuthentication  yes
```

#### 3.2.5.2 重启ssh服务

重启ssh服务：

```bash
~# service sshd restart
```

或者

```bash
~# systemctl  restart sshd
```

#### 3.2.5.3 生成Rsa公钥对

使用ssh-keygen命令在本地机器上生成Rsa公钥对：

```bash
~# ssh-keygen -t rsa
```

执行上述命令后，会提示输入要保存的文件路径，默认为：~/.ssh/id_rsa.

输入文件名，点回车，会提示输入秘钥的密码（会提示输入两遍），即可生成秘钥文件：

#### 3.2.5.4 上传Rsa公钥对

查看秘钥文件：

将公钥文件上传到服务上：

```bash
~# ssh-copy-id -i /home/zhao/.ssh/id_rsa_leilei.pub root@192.168.0.1
```

`-i` 是用来指定公钥文件，执行命令之后，按提示输入远程密码即可。 

然后即可使用私钥文件登录服务器：

```bash
~# ssh -i /home/zhao/.ssh/id_rsa_leilei   root@192.168.0.1
```

> 注意：如果在第3步时为秘钥设置了密码，则使用秘钥登录服务器时，需要输入秘钥密码。

### 3.2.6 ssh其他操作

1. 如果想实现免密登录，则只需要在第三步生成密钥对时不要设置秘钥密码。
2. 如果使用秘钥文件使用默认文件名（id_rsa），则在使用ssh的过程中就不需要再使用-i开关来指定秘钥文件了。
3. 拷贝文件到远程主机： ssh中提供了scp命令用来拷贝文件到远程主机，使用方式为：

```bash
~# scp -i /home/zhao/.ssh/id_rsa_miyao  a.tar.gz root@192.168.0.1:/home/zhao/
```

就能将文件 `a.tar.gz` 拷贝到远程主机`/home/zhao/`下。
在远程服务器上执行命令： 直接将需要执行的命令追加到ssh命令后面即可，如：

```bash
~# ssh -i /home/zhao/.ssh/id_rsa_miyao root@192.168.0.1  "ls -l"
```

即可在远程服务器上执行“`ls -l`” 命令，结果将输出到本地控制台。 但是在执行一些命令时，远程主机会提示无法找到该命令，这说明需要设置远程主机的环境变量，可在发送给远程主机的命令中增加source指令，如：

```bash
~# ssh -i /home/zhao/.ssh/id_rsa_miyao  root@192.168.0.1 "source ~/.bash_profile && ls -l"
```

注意：本文的命令示例中，均使用了 `-i` 开关来指定秘钥文件，如果使用默认秘钥文件：`~/.ssh/id_rsa`登录，则均可省略-i开关。



## 3.3 samba

### 3.3.1 samba（具体实现）

samba是一个基于GPL协议的自由软件。它重新实现了SMB/CIFS协议，可以在各个平台共享文件和打印机。

### 3.3.1 安装 samba

打开 ssh 连接Linux，输入如下命令:

```bash
sudo apt-get install samba
```

安装samba及其所有依赖。

### 3.3.1 配置samba.conf

可以直接修改/etc/samba/smb.conf，在文件末尾添加：

```
[share]
path = /home/pi
available = yes
browseable = yes
public = yes
writable = yes
```


每一行的意义，其英文都很明白。关键path要指定为你需要的文件夹。一般填写 /home/pi即可

### 3.3.1 添加samba账户

```bash
sudo touch /etc/samba/smbpasswd
sudo smbpasswd -a USER_NAME
```

USER_NAME就是你需要添加的用户名。然后会提示输入两次密码。

## 3.4 touch 

touch 的本意并非创建文件，而是

> **touch** — change file access and modification times *(BSD)*
> **touch** — change file timestamps *(GNU)*也就是摸一下好看上去最近动过了。

“修改文件的访问和修改时间”、“修改文件时间戳”。

## 3.5 NAS

NAS的定义是网络附属储存（Network Attached Storage），你可以把它理解成私人百度云盘，即私有云。通俗的说就是相当于家里一块巨大容量的硬盘，但是你并不需要随身携带，随时随地掏出手机或者笔记本都可以访问硬盘里的各种数据。本质上NAS就是一台电脑，只不过这电脑的配置、软件跟我们平时用的电脑不太一样。本质上nas就是一台小型长期不关机的服务器。

## 3.6 FTP

Samba只用于局域网，相当于windows的网上邻居。
ftp可以作服务器，其他人可以登录到你机子，下载或者上传东西。

### 3.6.1 FTP服务器

FTP服务器（File Transfer Protocol Server）是在互联网上提供文件存储和访问服务的计算机，它们依照FTP协议提供服务。 FTP是File Transfer Protocol(文件传输协议)。顾名思义，就是专门用来传输文件的协议。简单地说，支持FTP协议的服务器就是FTP服务器。

### 3.6.2 FTP（协议）

FTP是文件传输协议（File Transfer Protocol），用于在网络上进行文件传输的一套标准协议，使用客户/服务器模 式。专门用来传输文件的协议 。

### 3.6.3 认证模式

3.FTP服务器允许用户以三种认证模式登录到FTP服务器上:

匿名开放模式：是一种最不安全的认证模式，任何人都可以无需密码验证而直接登录到FTP服务器。

本地用户模式：是通过Linux系统本地的账户密码信息进行认证的模式，相较于匿名开放模式更安全，配置起 来也很简单。

虚拟用户模式：是这三种模式中最安全的一种认证模式，它需要为FTP服务单独建立用户数据库文件，虚拟出 用来进行口令验证的账户信息，而这些账户信息在服务器系统中实际上是不存在的 。

### 3.6.4 工作模式

FTP服务器工作模式

主动模式：FTP服务器主动向客户端发起连接请求

被动模式：FTP服务器等待客户端发起连接请求（FTP的默认工作模式）

端口：FTP协议默认使用20、21号端口，其中端口 20（数据端口）用于进行数据传输，端口21（命令端口）用于接受客户端发出的相关FTP命令与参数。



## 3.7 端口

有过一些黑客攻击方面知识的读者都会知道，其实那些所谓的黑客并不是像人们想象那样从天而降，而是实实在在从您的计算机"大门"中自由出入。计算机的"大门"就-是我们平常所说的"端口"，它包括计算机的`物理端口`，如计算机的串口、并口、输入/输出设备以及适配器接口等（这些端口都是可见的），但更多的是不可见的`软件端口`，在本文中所介绍的都是指"软件端口"，但为了说明方便，仍统称为"端口"。本文仅就端口的基础知识进行介绍，

### 3.7.1 端口简介

随着计算机网络技术的发展，原来物理上的接口（如键盘、鼠标、网卡、显示卡等输入/输出接口）已不能满足网络通信的要求，TCP/IP协议作为网络通信的标准协-议就解决了这个通信难题。TCP/IP协议集成到操作系统的内核中，这就相当于在操作系统中引入了一种新的输入/输出接口技术，因为在TCP/IP协议中引入了一种称之为"Socket（套接字）"应用程序接口。有了这样一种接口技术，一台计算机就可以通过软件的方式与任何一台具有Socket接口的计算机进行通信。端口在计算机编程上也就是`"Socket接口"`。

有了这些端口后，这些端口又是如何工作呢？例如一台服务器为什么可以同时是Web服务器，也可以是FTP服务器，还可以是邮件服务器等等呢？其中一个很重要的原因是各种服务采用不同的端口分别提供不同的服务，比如：通常TCP/IP协议规定Web采用80号端口，FTP采用21号端口等，而邮件服务器是采用25号端口。这样，通过不同端口，计算机就可以与外界进行互不干扰的通信。

### 3.7.2 端口分类

端口的分类根据其参考对象不同有不同划分方法，如果从端口的性质来分，通常可以分为以下三类：

（1）公认端口（Well Known Ports）：这类端口也常称之为"常用端口"。这类端口的端口号从0到1024，它们紧密绑定于一些特定的服务。通常这些端口的通信明确表明了某种服务的协议-，这种端口是不可再重新定义它的作用对象。例如：80端口实际上总是HTTP通信所使用的，而23号端口则是Telnet服务专用的。这些端口通常不会像木马这-样的黑客程序利用。为了使大家对这些常用端口多一些认识，在本章后面将详细把这些端口所对面应的服务进行列表，供各位理解和参考。

（2） 注册端口（Registered Ports）：端口号从1025到49151。它们松散地绑定于一些服务。也是说有许多服务绑定于这些端口，这些端口同样用于许多其他目的。这些端口多数没有明-确的定义服务对象，不同程序可根据实际需要自己定义，如后面要介绍的远程控制软件和木马程序中都会有这些端口的定义的。记住这些常见的程序端口在木马程序的防护-和查杀上是非常有必要的。常见木马所使用的端口在后面将有详细的列表。

（3） 动态和/或私有端口（Dynamic and/or Private Ports）：端口号从49152到65535。理论上，不应把常用服务分配在这些端口上。实际上，有些较为特殊的程序，特别是一些木马程序就非常喜欢用这些端-口，因为这些端口常常不被引起注意，容易隐蔽。

使用**TCP协议**的常见端口主要有以下几种：

（1） **FTP**：定义了文件传输协议，使用21端口。常说某某计算机开了FTP服务便是启动了文件传输服务。下载文件，上传主页，都要用到FTP服务。

（2） **Telnet**：它是一种用于远程登陆的端口，用户可以以自己的身份远程连接到计算机上，通过这种端口可以提供一种基于DOS模式下的通信服务。如以前的BBS是-纯字符界面的，支持BBS的服务器将23端口打开，对外提供服务。

（3） **SMTP**：定义了简单邮件传送协议，现在很多邮件服务器都用的是这个协议，用于发送邮件。如常见的免费邮件服务中用的就是这个邮件服务端口，所以在电子邮件设置-中常看到有这么SMTP端口设置这个栏，服务器开放的是25号端口。

（4） **POP3**：它是和SMTP对应，POP3用于接收邮件。通常情况下，POP3协议所用的是110端口。也是说，只要你有相应的使用POP3协议的程序（例如Fo-xmail或Outlook），就可以不以Web方式登陆进邮箱界面，直接用邮件程序就可以收到邮件（如是163邮箱就没有必要先进入网易网站，再进入自己的邮-箱来收信）。

使用**UDP协议端口**常见的有：

（1） **HTTP**：这是大家用得最多的协议，它就是常说的"超文本传输协议"。上网浏览网页时，就得在提供网页资源的计算机上打开80号端口以提供服务。常说"WWW服-务"、"Web服务器"用的就是这个端口。

（2） **DNS**：用于域名解析服务，这种服务在Windows

NT系统中用得最多的。因特网上的每一台计算机都有一个网络地址与之对应，这个地址是常说的IP地址，它以纯数字+"."的形式表示。然而这却不便记忆，于是出-现了域名，访问计算机的时候只需要知道域名，域名和IP地址之间的变换由DNS服务器来完成。DNS用的是53号端口。

（3） **SNMP**：简单网络管理协议，使用161号端口，是用来管理网络设备的。由于网络设备很多，无连接的服务就体现出其优势。

（4） **OICQ**：OICQ程序既接受服务，又提供服务，这样两个聊天的人才是平等的。OICQ用的是无连接的协议，也是说它用的是UDP协议。OICQ服务器是使用8-000号端口，侦听是否有信息到来，客户端使用4000号端口，向外发送信息。如果上述两个端口正在使用（有很多人同时和几个好友聊天），就顺序往上加。

### 3.7.3 端口的黑客应用

像木马之类的黑客程序，就是通过对端口的入侵来实现其目的的。在端口的利用上，黑客程序通常有两种方式，那就是"端口侦听"和"端口扫描"。

"端口侦听"与"端口扫描"是黑客攻击和防护中经常要用到的两种端口技术，在黑客攻击中利用它们可以准确地寻找攻击的目标，获取有用信息，在个人及网络防护方面，通过这种端口技术的应用可以及时发现黑客的攻击及一些安全漏洞。下面首先简单介绍一下这两种端口技术的异同。

"端口侦听"是利用某种程序对目标计算机的端口进行监视，查看目标计算机上有哪能些端口是空闲、可以利用的。通过侦听还可以捕获别人有用的信息，这主要是用在黑客软件中，但对于个人来说也是非常有用的，可以用侦听程序来保护自己的计算机，在`自己计算机的选定端口`进行监视，这样可以发现并拦截一些黑客的攻击。也可以侦听`别人计算机的指定端口`，看是否空闲，以便入侵。

"端口扫描"（port scanning）是通过连接到目标系统的TCP协议或UDP协议端口，来确定什么服务正在运行，然后获取相应的用户信息。现在有许多人把"端口侦听"与"端口-扫描"混为一谈，根本分不清什么样的情况下要用侦听技术，什么样的情况下要用扫描技术。不过，现在的这类软件也似乎对这两种技术有点模糊了，有的干脆把两个功能-都集成在一块。

"端口侦听"与"端口扫描"有相似之处，也有区别的地方，相似的地方是都可以对目标计算机进行监视，区别的地方是"端口侦听"属于一种`被动的过程`，等待别人的连接的出现，通过对方的连接才能侦听到需要的信息。在个人应用中，如果在设置了当侦听到有异常连接立即向用户报告这个功能时，就可以有效地侦听黑客的连接企图，及时把驻留在本机上的木马程序清除掉。这个侦听程序一般是安装在目标计算机上。用在黑客中的"端口侦听"通常是黑客程序驻留在服务器端等待服务器端在进行正常活动-时捕获黑客需要的信息，然后通过UDP协议无连接方式发出去。而"端口扫描"则是一种`主动过程`，它是主动对目标计算机的选定端口进行扫描，实时地发现所选定端口的所有活动（特别是对一些网上活动）。扫描程序一般是安装在客户端，但是它与服务器端的连接也主要是通过无连接方式的UDP协议连接进行。

在网络中，当信息进行传播的时候，可以利用工具，将网络接口设置在侦听的模式，便可将网络中正在传播的信息截获或者捕获到，从而进行攻击。端口侦听在网络中的任-何一个位置模式下都可实施进行，而黑客一般都是利用端口侦听来截取用户口令。

### 3.7.4 常用端口

在计算机的6万多个端口，通常把端口号为1024以内的称之为常用端口，这些常用端口所对应的服务通常情况下是固定的，所以了解这些常用端口在一定程序上是非常必要的。

代理服务器常用以下端口： 
（1）. HTTP协议代理服务器常用端口号：80/8080/3128/8081/9080 
（2）. SOCKS代理协议服务器常用端口号：1080 
（3）. FTP协议代理服务器常用端口号：21 
（4）. Telnet协议代理服务器常用端口：23

## 3.8 TCP/IP、Http、Socket区别

前两个是协议，但是layer 都不一样 。
而socket 完全不同的东西，是指通讯中的结点。

如果把主机比作一个房子，ip地址就类似于它房子的地址，应用程序类似于房子的好多房间，socket类似于应用程序的一个门，端口号类似于门牌号。
要准确地将数据投递到正确的房间，就需要从传输层的一个房子（主机）通过一个门（socket）进到应用层的一个房间（app）。

### 3.8.1 TCP/IP

tcp/ip是一个协议族，对应osi参考模型三层及以上层。

http是tcpip协议族的一个组成协议，是tcp的上层抽象。

### 3.8.2 Http

http是一种应用层协议，它使用tcp协议提供的服务。tcp协议是一种传输层协议，它使用ip协议提供的服务。ip协议是一种网络层协议。

### 3.8.3 Socket

对于Socket来说，面向网络的Sokcet其实就是主机IP地址+端口号，也就是xx.xx.xx.xx：xxxx就是一个Socket，Socket链接就是两个Socket之间建立的链接。

socket则是tcp/ip中运输层tcp和udp协议中的一个实现寻址的重要实现。具体来说，IP是用来定位网络上的一台计算机，那这台计算机上运行这好多服务怎么定位呢?答案就是socket。

# 4 工具和设置（侧重实际应用和技巧）

## 4.1 SSH连接云服务器

### 4.1.1 服务端设置

查看ssh服务的状态

```bash
service sshd status
```

#### 4.1.1.1 安装openssh-server

首先在服务器上安装SSH的服务器端。

```bash
apt-get install openssh-server
```

#### 4.1.1.2 启动ssh-server

```bash
service ssh start
```

#### 4.1.1.3 确认ssh-server

确认ssh-server是否正常工作

```shell
sudo ps -e | grep ssh-
```

说明`ssh-server`已经在运行了。

### 4.1.2 服务端设置

#### 4.1.2.1 通过SSH登录

在Ubuntu客户端通过SSH登录服务器。

假设服务器的IP地址是`113.112.23.124`，登录的用户名是`name`。

```shell
$ ssh -l name 113.112.23.124
```

#### 4.1.2.2 验证连接

最后提示你输入密码，就说明连上远程服务器了。



## 4.2 NFS服务器设置

Ubuntu 16.04 安装命令为：

```bash
# 服务端
apt install nfs-kernel-server
# 客户端
apt install nfs-common
```

### 4.2.1服务器端

1、修改 NFS 配置文件 `/etc/exports`

```bash
$ vim /etc/exports
/data/share 10.222.77.0/24(rw,sync,insecure,no_subtree_check,no_root_squash)
```

允许 IP 为该 `10.222.77.0/24` 区间的客户端挂载。

例如：

```
/home *(ro,sync,insecure,no_root_squash)
/share 192.168.1.*(rw,sync,insecure,no_subtree_check,no_root_squash)
```

| 参数             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| ro               | 只读访问                                                     |
| rw               | 读写访问                                                     |
| sync             | 所有数据在请求时写入共享                                     |
| async            | nfs在写入数据前可以响应请求                                  |
| secure           | nfs通过1024以下的安全TCP/IP端口发送                          |
| insecure         | nfs通过1024以上的端口发送                                    |
| wdelay           | 如果多个用户要写入nfs目录，则归组写入（默认）                |
| no_wdelay        | 如果多个用户要写入nfs目录，则立即写入，当使用async时，无需此设置 |
| hide             | 在nfs共享目录中不共享其子目录                                |
| no_hide          | 共享nfs目录的子目录                                          |
| subtree_check    | 如果共享/usr/bin之类的子目录时，强制nfs检查父目录的权限（默认） |
| no_subtree_check | 不检查父目录权限                                             |
| all_squash       | 共享文件的UID和GID映射匿名用户anonymous，适合公用目录        |
| no_all_squash    | 保留共享文件的UID和GID（默认）                               |
| root_squash      | root用户的所有请求映射成如anonymous用户一样的权限（默认）    |
| no_root_squash   | root用户具有根目录的完全管理访问权限                         |
| anonuid=xxx      | 指定nfs服务器/etc/passwd文件中匿名用户的UID                  |
| anongid=xxx      | 指定nfs服务器/etc/passwd文件中匿名用户的GID                  |

- 注1：尽量指定主机名或IP或IP段最小化授权可以访问NFS 挂载的资源的客户端
- 注2：经测试参数insecure必须要加，否则客户端挂载出错mount.nfs: access denied by server while mounting

2、执行命令使修改文件生效 

```bash
exprotfs -rv 
```

3、关闭服务端防火墙 

```bash
iptables -F
```

重启防火墙：service iptables restart   

查看状态：service iptables status

关闭防火墙：service iptables stop

4、启动服务：执行 

```bash
service nfs restart 
service portmap restart 
```

在服务端看下是否正确加载了设置的 `/etc/exports` 配置。

```bash
$ showmount -e localhost
Export list for localhost:
/data/share 10.222.77.0/24
```

可能遇到的问题：

ubuntu 10.0开启配置nfs 服务service nfs start时出现：Failed to start nfs.service: Unit nfs.service not found.

原因是ubuntu 10.0以上的版本取消了service nfs start。

改成了service nfs-server start 。这样就完成启动了。

在执行service nfs-server status就可以看到。

### 4.2.2客户端

测试，在另一台 Linux 虚拟机上测试一下，是否能够正确挂载吧。我们可以在客户端查看下 NFS 服务端 (上边服务端 IP 为：10.222.77.86) 设置可共享的目录信息。

```bash
showmount -e 10.222.77.86
Export list for 10.222.77.86:
/data/share 10.222.77.0/24
```

挂载执行命令： 
1、启动服务： 

```bash
service nfs restart 
service portmap restart 
```

2、 挂载

```bash
mount 172.16.203.246:/srv/www/app/wtcms/webroot/main /srv/www/app/wtweb/webroot/main -nolock -t nfs
```

其中，172.16.203.246 是服务端的ip    
/srv/www/app/wtcms/webroot/main  服务端共享的目录 
/srv/www/app/wtweb/webroot/main  客户端目录（一定要有此目录） 

3、取消挂载： 

```bash
umount  /srv/www/app/wtweb/webroot/main #（与mount一样的目录）   
```

客户端目录（一定要有此目录）  

# 5 软件配置（经验性设置、避坑）

## 5.1 关于配置，提高效率

网速更快啊，使用更爽、更流畅等等等。

### 5.1.1 anaconda源

channels:

- https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
- https://mirrors.sjtug.sjtu.edu.cn/anaconda/cloud/conda-forge/
- https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/free/
- defaults
  show_channel_urls: true

Linux下

将以上配置文件写在~/.condarc中 
vim ~/.condarc

```
channels:
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true
```

删源

换回conda的默认源。查看了conda config的文档后，发现直接删除channels即可。

conda config --remove-key channels

查看源
conda config --show



## 5.2 好用的工具

clover

ditto  

sourceinsight

notepad++

Typora

everything

pycharm

vscode

git

Mobaxtem

xshell

bitComet

Anaconda

snapnet



