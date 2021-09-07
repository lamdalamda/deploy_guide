<a name="index">**Index**</a>
&emsp;<a href="#0">System configuration record</a>  
<a href="#1">Hardware 硬件</a>  
&emsp;<a href="#2">e5 鸡血 @ z10pa</a>  
&emsp;<a href="#3">系统监测：</a>  
&emsp;<a href="#4">双路设置：</a>  
&emsp;<a href="#5">zbook17 changing to DC screen 换屏幕</a>  
&emsp;<a href="#6">nvme support</a>  
<a href="#7">Driver 安装驱动的那些事</a>  
&emsp;<a href="#8">install graphic card driver for unsupported graphic card 安装显卡驱动 zbook17</a>  
&emsp;<a href="#9">killer ax200</a>  
<a href="#10">windows system setting 系统设置</a>  
&emsp;<a href="#11">开启远程桌面:</a>  
&emsp;<a href="#12">windows照片查看器</a>  
&emsp;<a href="#13">a script for running android simulator 安卓模拟器等可以尝试</a>  
<a href="#14">windows to linux 远程操作linux </a>  
&emsp;<a href="#15">虚拟机注意事项</a>  
&emsp;&emsp;<a href="#16">vmware 使用的一些常用指令</a>  
&emsp;<a href="#17">wsl的基本设置</a>  
&emsp;&emsp;<a href="#18">双路主机：</a>  
&emsp;&emsp;<a href="#19">root 权限</a>  
&emsp;&emsp;<a href="#20">重启wsl</a>  
&emsp;<a href="#21">linux GUI</a>  
&emsp;<a href="#22">ssh通信</a>  
&emsp;&emsp;<a href="#23">vscode config 文件示例</a>  
&emsp;&emsp;<a href="#24">ssh免密码登录</a>  
&emsp;&emsp;<a href="#25">映射ssh的磁盘</a>  
<a href="#26">linux本身设置</a>  
&emsp;<a href="#27">basic linux command：</a>  
&emsp;<a href="#28">basic library</a>  
&emsp;&emsp;<a href="#29">ubuntu 18.04:</a>  
<a href="#30">python </a>  
&emsp;<a href="#31">environment 环境相关</a>  
&emsp;&emsp;<a href="#32">默认环境</a>  
&emsp;&emsp;<a href="#33">export the environment 导出环境:</a>  
&emsp;&emsp;<a href="#34">import environment from yml file 导入环境:</a>  
&emsp;&emsp;<a href="#35">a sample</a>  
&emsp;<a href="#36">library 库</a>  
&emsp;&emsp;<a href="#37">tensorflow:</a>  
&emsp;&emsp;&emsp;<a href="#38">tensorflow windows </a>  
&emsp;&emsp;&emsp;<a href="#39">test code for tensorflow tensorflow测试</a>  
&emsp;<a href="#40">实例</a>  
&emsp;&emsp;<a href="#41">监控网站信息变化，比如托福或者疫苗等</a>  
<a href="#42">Softwares 软件问题</a>  
&emsp;<a href="#43">vasp</a>  
&emsp;&emsp;<a href="#44">vasp build</a>  
&emsp;&emsp;<a href="#45">vasp cuda</a>  
&emsp;&emsp;<a href="#46">vasp bug</a>  
&emsp;&emsp;<a href="#47">vasp other</a>  
&emsp;&emsp;<a href="#48">vasp常用命令</a>  
&emsp;&emsp;<a href="#49">stopcar</a>  
&emsp;<a href="#50">git & github</a>  
&emsp;&emsp;<a href="#51">github ssh</a>  
&emsp;&emsp;<a href="#52">github clone</a>  
&emsp;&emsp;<a href="#53">GitHub page</a>  
&emsp;&emsp;<a href="#54">github page 目录</a>  
&emsp;<a href="#55">latex 配置</a>  
&emsp;&emsp;<a href="#56">latex中文支持</a>  
## <a name="0">System configuration record</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

**以下内容基本都是转载,如有侵权联系删除**

**declare no authorship to this page**



# <a name="1">Hardware 硬件</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>


## <a name="2">e5 鸡血 @ z10pa</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>


烧录器装好驱动https://item.taobao.com/item.htm?spm=a1z09.2.0.0.68162e8dApTxX1&id=592580392777&_u=n1ucmpp9f1e3
取下BIOS芯片，按照商家页面把bios芯片夹住，然后连usb。打开软件之后，先检测烧录器，然后打开鸡血bios （.cap），先擦除再写入（不知道需不需要擦除）。

电脑需要拔下电池，跳线到cmos重置模式半小时以上


刷好的bios芯片对着缺口插回去，尝试安装系统发现不可以用（卡在win10logo），于是在别的电脑上安装系统之后插回来，还是卡在了win10的logo。 重启三次之后进入安全模式选择禁用驱动程序强制签名，成功进去系统。

此时电脑上面是两个cpu，4条内存，一个nvme硬盘，连接了板载显卡，没有插独显

以这种方式进去系统之后，在系统里面双击win10安装程序，删除所有个人文件重装系统，安装完后系统正常工作，重启之后也正常

可以参考https://www.bilibili.com/read/cv4116433

之后是电源选择高性能，关闭快速启动，bios设定里面c state limie 设置成c0、c1，开启c3 report,禁用c6 report

再之后，格式化一个u盘，把  v3.efi 和 start.nsh放进去，引导这个优盘，让优盘把v3 efi相当于复制进系统的efi分区即可

## <a name="3">系统监测：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

千万不要用aida64，会导致功耗bug

使用hwinfo



## <a name="4">双路设置：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

只在1路插内存：即32g内存都在cpu1上面，cpuz跑分15w+

两路都插内存，总共64g，跑分10w

开启关闭虚拟化都是这样

关闭numa之后跑分回到15w+

而且在wsl相关性设置中，cpu 组1 变成了64个cpu，组2只有8个？？？？
原本是平均分配的


wtf？？？


## <a name="5">zbook17 changing to DC screen 换屏幕</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

https://forum.51nb.com/thread-1966563-1-1.html

2020.9新帖子，改30针屏线，没准可行！

目前已有是40针屏线，具有2lane定义，查看b173han04.0 和04.7似乎符合 40pin 2lane 

## <a name="6">nvme support</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

参照https://tieba.baidu.com/p/6282527282?see_lz=1
过程，使用clover来进行
先把原本硬盘数据备份到新盘，再备份回这个m.2
bios设置：
制作了clover的启动盘，可以加载nvme驱动并且引导系统
尝试把clover放进硬盘里面:

方法，对于目前的GPT硬盘，直接把EFI分区清空之后把200M的clover盘中文件全考进去，重启之后bios可以识别这个uefi并且引导出来就是clover


# <a name="7">Driver 安装驱动的那些事</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="8">install graphic card driver for unsupported graphic card 安装显卡驱动 zbook17</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

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

## <a name="9">killer ax200</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

https://bbs.luobotou.org/thread-45955-1-1.html11

# <a name="10">windows system setting 系统设置</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="11">开启远程桌面:</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

文件资源管理器,右键此电脑,跳出来设置的窗口,在相关设置里面有远程桌面,点进去打开

## <a name="12">windows照片查看器</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

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

## <a name="13">a script for running android simulator 安卓模拟器等可以尝试</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

启用：
```markdown

bcdedit /set hypervisorlaunchtype off
```

恢复：
```markdown

bcdedit /set hypervisorlaunchtype off
```

# <a name="14">windows to linux 远程操作linux </a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="15">虚拟机注意事项</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

安装vmhs-fuge还是啥的，为了虚拟机与实体机通信

虚拟机可以尝试使用固定ip

### <a name="16">vmware 使用的一些常用指令</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
`/usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other`



## <a name="17">wsl的基本设置</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="18">双路主机：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

可以任务管理器右键vmmm选择让wsl运行在哪个cpu上面

新发现：当关闭超线程之后，wsl可以同时在两个cpu中运行

注意可能需要重新安装libintel64？

性能测试

### <a name="19">root 权限</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

 `ubuntu1804.exe config --default-user root` 

打不开的时候：netsh winsock reset

### <a name="20">重启wsl</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`net stop LxssManager`
`net start LxssManager`

## <a name="21">linux GUI</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
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

## <a name="22">ssh通信</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="23">vscode config 文件示例</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

```markdown

Host 192.168.254.128
    HostName 192.168.254.128
    User root
    IdentityFile "C:\Users\（改成用户名）\.ssh\id_rsa"

```


### <a name="24">ssh免密码登录</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

Windows ssh 到 linux：

首先在service服务中，打开openssh，自动启动

ssh-keygen -t rsa (随便起个名字)

生成的pub放到linux机器的/.ssh下面，再把内容复制到./.ssh/authorized_keys里面

之后windows机器ssh-add 私钥名字

### <a name="25">映射ssh的磁盘</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

安装直接前往 github 对应项目的 release 中下载最新版本即可，需注意 sshfs-win 对 winfsp 的最低版本依赖（下载最新版本一般即可满足），另外有GUI（用户图形操作界面）可供下载

sshfs-win：https://github.com/billziss-gh/sshfs-win/releases
winfsp：https://github.com/billziss-gh/winfsp/releases

然后映射网络磁盘里面输入

\\sshfs\用户名@服务器名字\ 

后面不用加\home啥的，过去就相当于在\home\用户名底下

如果想要上层的话也可以

\\sshfs.r\用户名@服务器名字\home\用户名\.......

sshfs相当于省略\home\用户名的过程



# <a name="26">linux本身设置</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

最好用centos或者ubuntu18.04

## <a name="27">basic linux command：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

su / sudo ：管理员权限

sh xxxxx.sh :运行sh脚本

yum install / apt-get install : centos 和 ubuntu安装软件

`top`
查看cpu使用率

`top -u david`
查看用户的cpu使用率


`cat /proc/cpuinfo`
查看cpu型号核心数量

## <a name="28">basic library</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="29">ubuntu 18.04:</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`apt-get install build-essential gcc-multilib rpm lib32ncurses5 lib32z1`

# <a name="30">python </a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

先装好anaconda

## <a name="31">environment 环境相关</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="32">默认环境</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
在bashrc里添加
`conda activate environment name`

### <a name="33">export the environment 导出环境:</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`conda env export --name research > research.yml`


### <a name="34">import environment from yml file 导入环境:</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`conda env create -f environment.yml`

### <a name="35">a sample</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

https://github.com/lamdalamda/system-configure-record/blob/master/CARE/research.yml

## <a name="36">library 库</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
### <a name="37">tensorflow:</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
#### <a name="38">tensorflow windows </a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
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

#### <a name="39">test code for tensorflow tensorflow测试</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

```markdown
import tensorflow as tf
tf.config.list_physical_devices('GPU')
```

## <a name="40">实例</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="41">监控网站信息变化，比如托福或者疫苗等</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

同时具有发送邮件提醒功能

https://www.jianshu.com/p/7c4f251485b7?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

# <a name="42">Softwares 软件问题</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="43">vasp</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

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

### <a name="44">vasp build</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`OFLAG      = -O2 -xhost`
参考bilibili

`export PATH=$PATH:/root/repo/vasp.5.4.4/bin`

### <a name="45">vasp cuda</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

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

### <a name="46">vasp bug</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

**segmentation fault**

`ulimit -s 262140` 

至少需要incar poscar potcar kpoints才能运行

### <a name="47">vasp other</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

vasp6.1的GPU编译，新坑：https://zhuanlan.zhihu.com/p/302826820

### <a name="48">vasp常用命令</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

ulimit别忘了

### <a name="49">stopcar</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

stopcar 可以让计算在中途停止，只需要新建STOPCAR 文件 输入以下内容

```markdown
LSTOP = True

```

不知道跟这个有什么区别
`LABORT = .True.`

## <a name="50">git & github</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

对于新的os需要对git以及github进行设置

`git config --global user.name "lamdalamda"`

`git config --global user.email "邮箱"`

### <a name="51">github ssh</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

`ssh-keygen -t ed25519 -C "email address"`

`ssh-add ~/.ssh/id_ed25519`

再把pubkey复制到GitHub 设置里面的ssh keys里

之后可以进行正常使用

### <a name="52">github clone</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

对于需要pull 或者 push 到github的
如果是在vscode里面打开在点击pull或者push时候github扩展会跳出来打开chrome要求验证
也可以使用ssh登录，比较费劲

命令示例：
`git clone git@github.com:lamdalamda/deploy_guide.git`

### <a name="53">GitHub page</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

一般是在settings-page里面设定source在/docs 下面，然后建立docs文件夹，放进去index.html

如果用index.md使用markdown渲染出来，注意使用vscode插件markdown math和markdown preview enhanced

渲染出来html的话，在GitHub page上面不能显示正确的数学公式，需要在在<head>部分把原本的stylesheet部分换成以下代码
```markdown

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
```

这段代码会更新

_https://katex.org/docs/autorender.html_



### <a name="54">github page 目录</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

使用toc.py 搬运自https://github.com/Higurashi-kagome/pythontools/blob/master/text/toc.py

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

## <a name="55">latex 配置</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
### <a name="56">latex中文支持</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
参考https://zhuanlan.zhihu.com/p/43133114


对于latex workshop插件，在visual studio code的settings.json 里面添加如下内容

```markdown
    // Latex workshop
    "latex-workshop.latex.tools": [
          {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "%DOC%"
            ]
          },
          {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
              ]
          },          
          {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
            ]
          },
          {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
            "%DOCFILE%"
            ]
          }
        ],
    "latex-workshop.latex.recipes": [
          {
            "name": "xelatex",
            "tools": [
            "xelatex"
                        ]
                  },
          {
            "name": "latexmk",
            "tools": [
            "latexmk"
                        ]
          },

          {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
            "pdflatex",
            "bibtex",
            "pdflatex",
            "pdflatex"
                        ]
          }
        ],
    "latex-workshop.view.pdf.viewer": "tab",  
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk"
      ]
```