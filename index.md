## System configuration record

**以下内容基本都是转载,如有侵权联系删除**

**declare no authorship to this page**

# Hardware 硬件


## e5 鸡血 @ z10pa


烧录器装好驱动https://item.taobao.com/item.htm?spm=a1z09.2.0.0.68162e8dApTxX1&id=592580392777&_u=n1ucmpp9f1e3
取下BIOS芯片，按照商家页面把bios芯片夹住，然后连usb。打开软件之后，先检测烧录器，然后打开鸡血bios （.cap），先擦除再写入（不知道需不需要擦除）。

电脑需要拔下电池，跳线到cmos重置模式半小时以上


刷好的bios芯片对着缺口插回去，尝试安装系统发现不可以用（卡在win10logo），于是在别的电脑上安装系统之后插回来，还是卡在了win10的logo。 重启三次之后进入安全模式选择禁用驱动程序强制签名，成功进去系统。

此时电脑上面是两个cpu，4条内存，一个nvme硬盘，连接了板载显卡，没有插独显

以这种方式进去系统之后，在系统里面双击win10安装程序，删除所有个人文件重装系统，安装完后系统正常工作，重启之后也正常

可以参考https://www.bilibili.com/read/cv4116433

之后是电源选择高性能，关闭快速启动，bios设定里面c state limie 设置成c0、c1，开启c3 report,禁用c6 report

再之后，格式化一个u盘，把  v3.efi 和 start.nsh放进去，引导这个优盘，让优盘把v3 efi相当于复制进系统的efi分区即可



## zbook17 changing to DC screen 换屏幕

https://forum.51nb.com/thread-1966563-1-1.html

2020.9新帖子，改30针屏线，没准可行！

目前已有是40针屏线，具有2lane定义，查看b173han04.0 和04.7似乎符合 40pin 2lane 

## nvme support

参照https://tieba.baidu.com/p/6282527282?see_lz=1
过程，使用clover来进行
先把原本硬盘数据备份到新盘，再备份回这个m.2
bios设置：
制作了clover的启动盘，可以加载nvme驱动并且引导系统
尝试把clover放进硬盘里面:

方法，对于目前的GPT硬盘，直接把EFI分区清空之后把200M的clover盘中文件全考进去，重启之后bios可以识别这个uefi并且引导出来就是clover


# Driver 安装驱动的那些事

## install graphic card driver for unsupported graphic card 安装显卡驱动 zbook17

zbook17显卡：
根据网上，只支持到p5200?

更换--》简单，用热风枪吹掉显卡支架，
记得bios开启混合显卡模式

驱动：
直接下载最新exe驱动，右键解压，卸载所有nvidia驱动，用driver cleaner再清除一遍，然后设备管理器-microsoft基本适配器
然后安装，从磁盘安装，找到那个inf（是bli结尾的？）。我是安装之前改好了inf，不确定需不需要改inf

inf更改：
首先设备管理器找到显卡硬件id，然后再nVidia驱动解压出来的文件里面 找惠普对应的（103C结尾，应该是bli之类的inf）
禁用设备签名（设置里面，恢复，高级重新启动），然后inf右键安装

## killer ax200

https://bbs.luobotou.org/thread-45955-1-1.html11

# windows system setting 系统设置

## 开启远程桌面:

文件资源管理器,右键此电脑,跳出来设置的窗口,在相关设置里面有远程桌面,点进去打开

## windows照片查看器

保存成reg文件双击运行

```markdown
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Photo Viewer\Capabilities\FileAssociations]
 ".jpg"="PhotoViewer.FileAssoc.Tiff"
 ".jpeg"="PhotoViewer.FileAssoc.Tiff"
 ".bmp"="PhotoViewer.FileAssoc.Tiff"
 ".png"="PhotoViewer.FileAssoc.Tiff"
 ".ico"="PhotoViewer.FileAssoc.Tiff"
 ".jpe"="PhotoViewer.FileAssoc.Tiff"
 ".dib"="PhotoViewer.FileAssoc.Tiff"
 ".jfif"="PhotoViewer.FileAssoc.Tiff"
 ".wdp"="PhotoViewer.FileAssoc.Tiff"
```

## a script for running android simulator 安卓模拟器等可以尝试

启用：
```markdown

bcdedit /set hypervisorlaunchtype off
```

恢复：
```markdown

bcdedit /set hypervisorlaunchtype off
```

# windows to linux 远程操作linux 

## 虚拟机注意事项

安装vmhs-fuge还是啥的，为了虚拟机与实体机通信

虚拟机可以尝试使用固定ip

### vmware 使用的一些常用指令
`/usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other`



## wsl的基本设置

### root 权限

 `ubuntu1804.exe config --default-user root` 

打不开的时候：netsh winsock reset

## linux GUI
GUI-xfce
https://zhuanlan.zhihu.com/p/150555651
RDP:
https://zhuanlan.zhihu.com/p/149501381
显示GUI

**某个具体过程（通过xfce4实现）**

`sudo apt-get install xfce4`

.bashrc中添加：

`export DISPLAY=:0.0`


之后下载并安装 VcXsrv Windows X Server

https://sourceforge.net/projects/vcxsrv/

Windows X-server based on the xorg git sources (like xming or cygwin's xwin), but compiled with Visual C++ 2012 Express Edition. Source code can also be compiled with VS2008, VS2008 Express Edition and VS2010 Express Edition, although current project and makefile are not fully compatible anymore.

 先启动 XLaunch

 再在 WSL 中启动 Xfce 会话

`startxfce4`

## ssh通信

### vscode config 文件示例

```markdown

Host 192.168.254.128
    HostName 192.168.254.128
    User root
    IdentityFile "C:\Users\（改成用户名）\.ssh\id_rsa"

```


### ssh免密码登录

Windows ssh 到 linux：

首先在service服务中，打开openssh，自动启动

ssh-keygen -t rsa (随便起个名字)

生成的pub放到linux机器的/.ssh下面，再把内容复制到./.ssh/authorized_keys里面

之后windows机器ssh-add 私钥名字

### 映射ssh的磁盘

安装直接前往 github 对应项目的 release 中下载最新版本即可，需注意 sshfs-win 对 winfsp 的最低版本依赖（下载最新版本一般即可满足），另外有GUI（用户图形操作界面）可供下载

sshfs-win：https://github.com/billziss-gh/sshfs-win/releases
winfsp：https://github.com/billziss-gh/winfsp/releases

然后映射网络磁盘里面输入

\\sshfs\用户名@服务器名字\ 

后面不用加\home啥的，过去就相当于在\home\用户名底下

如果想要上层的话也可以

\\sshfs.r\用户名@服务器名字\home\用户名\.......

sshfs相当于省略\home\用户名的过程



# linux本身设置

最好用centos或者ubuntu18.04

## basic linux command：

su / sudo ：管理员权限

sh xxxxx.sh :运行sh脚本

yum install / apt-get install : centos 和 ubuntu安装软件

## basic library

### ubuntu 18.04:

`apt-get install build-essential gcc-multilib rpm lib32ncurses5 lib32z1`

# python 

先装好anaconda

## environment 环境相关

### export the environment 导出环境:

`conda env export --name research > research.yml`


### import environment from yml file 导入环境:

`conda env create -f environment.yml`

### a sample

https://github.com/lamdalamda/system-configure-record/blob/master/CARE/research.yml

## library 库
### tensorflow:
#### tensorflow windows 
假设tensorflow安装在D:\Anaconda3\Lib\site-packages\tensorflow环境里，那么打开D:\Anaconda3\Lib\site-packages\tensorflow\python\platform\build_info.py这个文件

检查一下默认写好的系统变量CUDA_PATH和CUDA_PATH_V9.0是否无误


检查一下系统变量path中是否有NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin和NVIDIA GPU Computing Toolkit\CUDA\v9.0\lib\x64并且正确。
默认路径如下：
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\lib\x64

直接pip install tensorflow就行，有错误改错误

tensorflow-cuda：需要找到tensorflow对应的cuda，cudnn

下载下来之后安装，放在环境变量里面，缺什么加什么
官网版本未必对应，可以看安装后缺少的dll版本

#### test code for tensorflow tensorflow测试

```markdown
import tensorflow as tf
tf.config.list_physical_devices('GPU')
```

# build software 在linux中编译软件的问题

## vasp

首先：安装intel oneapi

会更新

base要安装 hpctookit不知道需不需要

wget https://registrationcenter-download.intel.com/akdlm/irc_nas/17977/l_BaseKit_p_2021.3.0.3219_offline.sh
wget https://registrationcenter-download.intel.com/akdlm/irc_nas/17764/l_HPCKit_p_2021.2.0.2997_offline.sh 

sh 运行下载好的包，安装oneapi

之后要source 一下，参考intel的start guide
在.bashrc里面
`source /opt/intel/oneapi/setvars.sh`


**make libintel64** 如果是默认路径

`cd /opt/intel/oneapi/mkl/2021.3.0/interfaces/fftw3xf/ `
`make libintel64`

### vasp build

`OFLAG      = -O2 -xhost`
参考bilibili

### vasp cuda

CUDA在makefile include里面要改
`GENCODE_ARCH    := -gencode=arch=compute_52,code=\"sm_52,compute_52\"` 

报错icc: command line error: option '-openmp' is not supported. Please use the replacement option '-qopenmp'

解决后
再报错找不到mpi.h
尝试吧makefile.include中改成
`MPI_INC    = $(I_MPI_ROOT)/intel64/include`


也可以尝试sudo apt install libopenmpi-dev，但还没试

再报错，
查看了一下，cuda root 指向CUDA_ROOT  ?= /usr/local/cuda/，这个cuda指向了\\wsl\Ubuntu-18.04\usr\local\cuda-11.0\targets\x86_64-linux\lib，然后-lcuda不能运行是因为没有libcuda.so。 这个文件被放在了stub文件夹里，还有libnvidia-ml也被放了进去，所以复制了出来

总之找不到什么文件就搜索一下然后指一下路径

### vasp bug

**segmentation fault**

`ulimit -s 262140` 

或者更大的数

`ulimit -u unlimited`


至少需要incar poscar potcar kpoints才能运行




```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/lamdalamda/deploy_guide/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
