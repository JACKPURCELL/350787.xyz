---
title: "Clion + Ubuntu远程调试"
subtitle: "在Ubuntu上编译运行，避免扯蛋问题"
layout: post
author: "LJC"
header-style: text
catalog: true
tags: 
- Tips 
- Clion 
- C 
- Ubuntu 
- MAC
---

最近大家都苦于计网和操作系统实验的编译环境，不少都开着虚拟机写代码，实在憋屈，由于之前要用到OPENSSL和BOOST库，所有整了这个远程调试，后来都用远程调试编译了。

## 工具

+ 配有Clion的MAC或者Windows电脑
+ 有一台云服务器

## 准备

### 给ECS安装gcc、g++、make

```shell
sudo apt-get install build-essential
```

### 给ECS安装CMAKE最新版

```sh
sudo apt-get install libssl-dev
wget https://cmake.org/files/v3.17/cmake-3.17.0.tar.gz
tar -xvf cmake-3.17.0.tar.gz
cd cmake-3.17.0
./configure
sudo make
sudo make install
hash -r
cmake --version
```

### 给ECS安装gdb

```shell
sudo apt-get install gdb
```

## 配置

先整个新的Hello World方便配置

![clion_newproject](https://md.350787.xyz/clion_newproject.png)

然后进入Preference ,点击+号添加自己的主机信息

![clion_toolchain1](https://md.350787.xyz/clion_toolchain1.png)

配置完成后如图，一般下面的路径建议直接手动输入，不建议选用Detect

![clion_shell](https://md.350787.xyz/clion_shell.png)

![clion_toolchain2](https://md.350787.xyz/clion_tag.png)

然后点击Cmake，勾选上方的自动重新加载Cmake项目，并且把工具链改成刚刚设置的主机

![clion_cmake](https://md.350787.xyz/clion_change2.png)

<img src="https://md.350787.xyz/clion_cmake.png" alt="clion_change2" style="zoom:50%;" />

最后记得打开自动上传

![clion_auto](https://md.350787.xyz/clion_toolchain2.png)

## 实际使用

然后就配置完成啦，看看右上方的tag是否变成远程主机

![clion_tag](https://md.350787.xyz/clion_finash.png)

刚配置完第一次加在Cmake会很慢，后面就不会了

![clion_start](https://md.350787.xyz/clion_change.png)



好了，加载完毕了，点击运行看看

![clion_finash](https://md.350787.xyz/clion_start.png)



再修改看看，不用按保存，直接点击运行，测试下自动上传是否运行正常。

![clion_change](https://md.350787.xyz/clion_auto.png)

大功告成



## 下次使用

只要把工具链改了，再把自动加载Cmake跟自动上传勾选上就完事了！

![clion_change2](https://md.350787.xyz/clion_cmake.png)



### 快来体验Ubuntu编译的快乐吧！





附：使用多线程时记得在Cmakelists加上

```shell
link_libraries(pthread)
```

