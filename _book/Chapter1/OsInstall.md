# 系统安装

## WSL方案

### 安装方法

wsl(Windows Subsystem for Linux)是一个为在windows10上原生运行Linux二进制可执行文件的兼容层，简单来说就是我们可以在windows10系统中使用linux系统。安装方法如下：

1. 找到 控制面板=>程序=>启用或关闭windows功能=>适用于Linux的Windows子系统，选中并确定；
2. 打开 Microsoft Store，搜索linux，会出现一系列的应用程序，这里推荐安装Ubuntu（后续教程都以Ubuntu系统为例）（Ubuntu 18.04.4 LTS）；
3. 傻瓜式安装完成后我们可以在开始菜单中找到安装好的Ubuntu，第一次启动时会要求设置UNIX username和UNIX password（请牢记），至此我们已经在windows10上成功安装了wsl。

### 优点&缺点

优点就不多说，主要是简单方便快捷，缺点是wsl1还有些缺陷，不能运行docker、cuda等，不过这些一般用不上。

## 虚拟机方案

### 安装方法

1. 下载VMware Workstation Player（免费软件，也有对应的功能更强大的VMware Workstation Pro）或者是VirtualBox（免费软件）；

2. 下载Ubuntu 18.04.4 LTS（推荐这个版本），不同版本一些操作可能不太一样；

   这里有几个国内的镜像下载地址：

   ​	a. [网易163源](http://mirrors.163.com/ubuntu-releases/18.04.4/ubuntu-18.04.4-desktop-amd64.iso)

   ​	b. [中科大源](http://mirrors.ustc.edu.cn/ubuntu-releases/18.04.4/ubuntu-18.04.4-desktop-amd64.iso)

   ​	c. [阿里源](http://mirrors.aliyun.com/ubuntu-releases/18.04.4/ubuntu-18.04.4-desktop-amd64.iso)

   ​	d. [浙大源](http://mirrors.zju.edu.cn/ubuntu-releases/18.04.4/ubuntu-18.04.4-desktop-amd64.iso)

3. 用必应/百度搜索如何用你下载的虚拟机软件（VMware/VirtualBox）安装系统。

### 优点&缺点

个人认为优点是更加原生的体验，docker啥的也可以运行，但是虚拟机目前无法连接显卡，所以cuda啥的也是没法用的。

## 多系统方案

在原有的系统上多安装一个系统可以获得更好的体验，大致方法是下载操作系统的iso文件，然后用软碟通等软件制作启动盘，在启动电脑的时候进入BIOS，选择从U盘（USB Device）启动，然后安装提示即可安装。具体方法还请自行必应/百度搜索。