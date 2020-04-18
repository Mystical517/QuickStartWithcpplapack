# 环境配置

安装完操作系统了，我们要配置环境，以期编译c/c++、调用lapack。

以下教程需要linux系统基本操作命令(ls、cd、vi/vim等等)以及您使用的Linux发行版本如何安装程序，如果您对此并不了解，可以跟着以下教程先大致的学一下：

1. [Linux 文件基本属性 | 菜鸟教程](https://www.runoob.com/linux/linux-file-attr-permission.html)
2. [Linux 文件与目录管理 | 菜鸟教程](https://www.runoob.com/linux/linux-file-content-manage.html)
3. [Linux vi/vim | 菜鸟教程](https://www.runoob.com/linux/linux-vim.html)

**以下教程均基于Ubuntu 18.04 LTS**

## 软件源配置
Ubuntu系统默认的软件源在国外，下载速度很慢，所以我们要把他换成国内的软件源（软件源可以简单的理解为类似手机上的应用商店），这里推荐使用清华大学的软件源或者是阿里云的软件源。

[清华大学软件源](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/)
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

[阿里云软件源](https://developer.aliyun.com/mirror/ubuntu)

```
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```


### 具体步骤

```shell
sudo mv /etc/apt/sources.list /etc/apt/sources.list.bak #这一步是将原有的配置文件备份
sudo vim /etc/apt/sources.list #这一步是编辑（创建）配置文件
# 将上软件源粘贴进配置文件，保存并退出。若不会操作请参考上`Linux vi/vim | 菜鸟教程`或自行搜索
sudo apt update #按照配置文件更新
```

*（粘贴时不要包括#号及其后内容！！！）*

至此已经换源成功。如果update时出现报错，大概率是换错版本了，建议先使用`lsb_release -a`查看系统版本，然后去软件源官网找相应的软件源


## c/c++环境配置
在终端中依次输入以下命令：
```shell
sudo apt-get install gcc
sudo apt-get install g++
```

至此c/c++环境已经配置好了，我们可以试一下***Hello，world！***

```c++
// hello.cpp
#include<iostream>

using namespace std;

int main(){
    cout<<"Hello, world!"<<endl;
    return 0;
}
```

保存并退出，用`g++ -o hello hello.cpp`编译，等编译结束后用`./hello`运行编译得到的文件（如下图）。

![image-20200418201426873](..\images\image-20200418201426873.png)

至此，恭喜你已经成功一大半了！:smile:

## cpplapack使用环境配置

下将依次介绍什么是blas&lapack、什么是cpplapack、如何安装blas&lapack以及如何使用cpplapack。

### 介绍

#### blas&lapack

**BLAS(Basic Linear Algebra Subprograms)：**基础线性代数子程序库，内集成了大量线性代数运算的程序。

[BLAS官网地址](http://www.netlib.org/lapack/)

**LAPACK(Linear Algebra PACKage)：** Fortran编写的一套数值计算函数库，内集成了求解常见数值线性代数问题的函数，如特征值问题、奇异值问题、线性方程组和最小二乘等。

[LAPACK官网地址](http://www.netlib.org/blas/)

#### cpplapack

cpplapack是赵继泽老师写的调用blas&lapack的一系列接口文件，简化了一些常用函数的调用方式，并且重载了不少常用函数。使用cpplapack会使不少功能实现起来方便不少。

### 具体步骤

#### blas&lapack环境配置

首先感谢一下2018物理二班/物理学萃英班的田西城同学，这部分主要参考他提供的教程。[传送门](https://www.assistedcoding.eu/2017/11/04/how-to-install-lapacke-ubuntu/)

虽然上面资料是英文的，但是不要害怕，很简单。

懒得看的同学也可以直接在终端依次输以下命令就完事儿了:

```shell
sudo apt install liblapack3
sudo apt install liblapack-dev
sudo apt install libopenblas-base
sudo apt install libopenblas-dev
sudo apt install liblapacke-dev
```

至此我们完成了lapack的安装，头文件里应该已经有了`cblas.h`和`lapacke.h`,至此我们已经可以在c/c++中调用blas和lapack。

如果您有兴趣尝试cblas和lapacke，他们的官网有详细的说明文档。

#### cpplapack使用

 blas和lapack是fortran实现的，要调用他们我们得先安装fortran的编译器gfortran,使用以下命令安装：

```shell
sudo apt-get install gfortran
```

然后我们要下载cpplapak，【此处留空】

之后我们要使用cpplapack只需将cpplapack拷贝到要使用的目录下，引用要用函数所在的头文件，在编译的时候带上对应的链接文件(*.o)即可。

在下一章，我们会讲解cpplapack中有哪些函数以及他们的用法，并配合示例代码及编译方式。



