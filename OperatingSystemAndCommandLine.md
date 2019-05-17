

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



# 2 Windows



# 3 底层基础

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

## 3.2.6 ssh其他操作

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

# 3.8 TCP/IP、Http、Socket区别

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

1=tcpmux（TCP协议 Port Service

Multiplexer）401=ups（Uninterruptible Power

Supply）

2=compressnet=Management Utility402=genie（Genie Protocol）

3=compressnet=Compression Process403=decap

5=rje（Remote Job Entry）404=nced

7=echo=Echo405=ncld

9=discard406=imsp（Interactive Mail Support Protocol）

11=systat,Active Users407=timbuktu

13=daytime408=prm-sm（Prospero Resource Manager Sys. Man.）

17=qotd（Quote of the Day）409=prm-nm（Prospero Resource Manager

Node Man.）

18=msp（Message Send Protocol）410=decladebug（DECLadebug Remote

Debug

Protocol）

19=Character Generator411=rmt（Remote MT Protocol）

20=FTP-data（File Transfer [Default

Data]）412=synoptics-trap（Trap

Convention Port）

21=FTP（File Transfer [Control]）413=smsp

22=ssh414=infoseek

23=telnet415=bnet

24private mail system416=silverplatter

25=smtp（Simple Mail Transfer）417=onmux

27=nsw-fe（NSW User System FE）418=hyper-g

29=msg-icp419=ariel1

31=msg-auth420=smpte

33=Display Support Protocol421=ariel2

35=private printer server422=ariel3

37=time423=opc-job-start（IBM Operations Planning and Control

Start）

38=rap（Route Access Protocol）424=opc-job-track（IBM Operations

Planning and

Control Track）

39=rlp（Resource Location Protocol）425=icad-el（ICAD）

41=graphics426=smartsdp

42=nameserver（WINS Host Name Server）427=svrloc（Server

Location）

43=nicname（Who Is）428=ocs_cmu

44=mpm-flags（MPM FLAGS Protocol）429=ocs_amu

45=mpm（Message Processing Module [recv]）430=utmpsd

46=mpm-snd（MPM [default send]）431=utmpcd

47=ni-ftp432=iasd

48=Digital Audit Daemon433=nnsp

49=tacacs（Login Host Protocol （TACACS））434=mobileip-agent

50=re-mail-ck（Remote Mail Checking Protocol）435=mobilip-mn

51=la-maint（IMP Logical Address Maintenance）436=dna-cml

52=xns-time（XNS Time Protocol）437=comscm

53=Domain Name Server438=dsfgw

54=xns-ch（XNS Clearinghouse）439=dasp（dasp Thomas Obermair）

55=isi-gl（ISI Graphics Language）440=sgcp

56=xns-auth（XNS Authentication）441=decvms-sysmgt

57= private terminal access442=cvc_hostd

58=xns-mail（XNS Mail）443=https（https Mcom）

59=private file service444=snpp（Simple Network Paging Protocol）

61=ni-mail（NI MAIL）445=microsoft-ds

62=acas（ACA Services）446=ddm-rdb

63=whois+whois+447=ddm-dfm

64=covia（Communications Integrator （CI））448=ddm-byte

65=tacacs-ds（TACACS-Database Service）449=as-servermap

66=sql*net（Oracle SQL*NET）450=tserver

67=bootps（Bootstrap Protocol Server）451=sfs-smp-net（Cray

Network Semaphore

server）

68=bootpc（Bootstrap Protocol Client）452=sfs-config（Cray SFS

config server）

69=tftp（Trivial File Transfer）453=creativeserver

70=gopher454=contentserver

71=netrjs-1,Remote Job Service455=creativepartnr

72=netrjs-2,Remote Job Service456=macon-tcp

73=netrjs-3,Remote Job Service457=scohelp

74=netrjs-4,Remote Job Service458=appleqtc（apple quick time）

75=private dial out service459=ampr-rcmd

76=deos（Distributed External Object Store）460=skronk

77=private RJE service461=datasurfsrv

78=vettcp462=datasurfsrvsec

79=finger463=alpes

80=http（World Wide Web HTTP）464=kpasswd

81=hosts2-ns（HOSTS2 Name Server）465=ssmtp

82=xfer（XFER Utility）466=digital-vrc

83=mit-ml-dev（MIT ML Device）467=mylex-mapd

84=ctf（Common Trace Facility）468=photuris

85=mit-ml-dev（MIT ML Device）469=rcp（Radio Control Protocol）

86=mfcobol（Micro Focus Cobol）470=scx-proxy

&nbs

# 4 工具和设置

## 4.1 SSH连接云服务器

### 4.1.1 服务端设置

#### 4.1.1.1 安装openssh-server

首先在服务器上安装SSH的服务器端。

```
$ sudo aptitude install openssh-server
```

#### 4.1.1.2 启动ssh-server

```
$ /etc/init.d/ssh restart
```

#### 4.1.1.3 确认ssh-server

确认ssh-server是否正常工作

```shell
$ netstat -tlp
tcp6 0 0 *:ssh *:* LISTEN -
```

上面这一行就说明`ssh-server`已经在运行了。

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

NFS服务器的设定可以通过/etc/exports这个文件进行，设定格式如下：

分享目录      主机名称或者IP(参数1，参数2）

/arm2410s   10.22.22.*(rw,sync,no_root_squash)

可以设定的参数主要有以下这些：

rw：可读写的权限； 
ro：只读的权限； 
no_root_squash：登入到NFS主机的用户如果是root，该用户即拥有root权限；
root_squash：登入NFS主机的用户如果是root，该用户权限将被限定为匿名使用者nobody； 
all_squash：不管登陆NFS主机的用户是何权限都会被重新设定为匿名使用者nobody。 
anonuid：将登入NFS主机的用户都设定成指定的user id，此ID必须存在于/etc/passwd中。 
anongid：同anonuid，但是变成group ID就是了！ 
sync：资料同步写入存储器中。 
async：资料会先暂时存放在内存中，不会直接写入硬盘。 
insecure：允许从这台机器过来的非授权访问。 

例如可以编辑/etc/exports为： 
/tmp　　　　　*(rw,no_root_squash) 
/home/public　192.168.0.*(rw)　　 *(ro) 
/home/test　　192.168.0.100(rw) 
/home/linux　 *.the9.com(rw,all_squash,anonuid=40,anongid=40) 

# 5 软件配置

## 5.1 anaconda源

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



