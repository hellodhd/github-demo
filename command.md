source /etc/profile

ubuntu: 查看cuda版本
nvcc -V

查看当前Ubuntu系统的版本
使用命令：uname -a 查看



1、在终端输入$sudo gedit /etc/profile，打开profile文件，profile是系统级的环境

2、在文件末尾添加一行：

export  PATH=/home/grant/anaconda2/bin:$PATH，其中，
将“/home/grant/anaconda2/bin”替换为你实际的安装路径，保存。
3. 使环境变量生效
方法1：
让/etc/profile文件修改后立即生效 ,可以使用如下命令:
# .  /etc/profile
注意: . 和 /etc/profile 有空格
方法2：
让/etc/profile文件修改后立即生效 ,可以使用如下命令:
# source /etc/profile

channels:
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true

Linux下


将以上配置文件写在~/.condarc中 
vim ~/.condarc

    channels:
      - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
      - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
      - defaults
    show_channel_urls: true


 
删源

换回conda的默认源。查看了conda config的文档后，发现直接删除channels即可。

conda config --remove-key channels


查看源
conda config --show
