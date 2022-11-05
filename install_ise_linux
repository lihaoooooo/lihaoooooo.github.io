# 记一次配环境经历

这次配环境主要是重装了Win10和ubuntu20.04两个系统，同时在Linux环境中将Xilinx ISE套件配置好。在此记录一些操作，以免遗忘。

- - - - - -

警告：装系统、磁盘分区等操作有丢失文件的风险，如果想自己动手装系统，请先备份好自己的重要文件，做好所有文件丢失的准备

- - - - - -

## 起因

听说在linux环境下ise综合速度会加快，而且不会有win10环境下各种各样奇怪的bug，所以想把ise装到linux上。然而最开始装双系统的时候只给ubuntu分配了30G的空间，已经不够了，想买一块硬盘做拓展，发现自己的笔记本只有一个硬盘插槽，于是决定重新对硬盘分区，然后重装系统，之后再把ise装上去。

## 大概的步骤

### 重装系统

- 删除ubuntu所在分区，删除ubuntu的启动引导
- 在磁盘管理将空分区分配回win10
- 运行win10的系统重装功能
- 在win10下用磁盘管理分配新的大分区给ubuntu
- 用烧录了ubuntu系统镜像的u盘启动，安装ubuntu到新分区
- 简单配置一下新装好的系统

### 安装配置ise(在ubuntu20.04下)

- 下载ise14.7linux包
- 安装，发现usb cable安装失败，但是其他组件都安装成功了
- 写一个简单脚本，配置ise的启动
- 初次启动ise，加载证书
- 通过其他方法安装usb cable驱动*

## 遇到的各种坑

- ubuntu安装时如果选用覆盖原系统安装，会触发win10的bitlock验证，需要输入秘钥才能解锁
- 新装好的ubuntu对nvidia显卡的支持有奇奇怪怪的问题，有几率开机触发ppm failed错误导致无法开机
- ise安装时会缺失一些库，需要手动安装
- ise安装好之后第一次打开如果没有配置好证书，之后打开时候会在证书验证的过程中触发段错误，导致永远无法打开
- ise的驱动在ubuntu系统一定会安装失败，需要手动安装环境、安装驱动。

## 详细过程

### 删ubuntu

见此博客 [https://blog.csdn.net/lele_god/article/details/109046860](https://blog.csdn.net/lele_god/article/details/109046860)
需要注意按此流程删除后，需要进入win10的磁盘管理，对空分区使用拓展卷功能。

### win10重装

见此网页 [http://robotrs.lenovo.com.cn/ZmptY2NtYW5hZ2Vy/p4data/Rdata/Rfiles/203.html](http://robotrs.lenovo.com.cn/ZmptY2NtYW5hZ2Vy/p4data/Rdata/Rfiles/203.html)
在高级重启后进入疑难解答选择重置此电脑（注意，这会删除掉所有文件，请先备份好重要文件）

### 装ubuntu

用u盘启动，安装到之前分配的空分区即可。

### 配置系统

装一些基础的工具、换源。
针对开机ppm fails错误的问题，网上没有太全面的解决方法，搜索时只搜到一篇stackoverflow上的问答 [https://askubuntu.com/questions/1210411/failed-to-init-ppm-ppm-reset-failed-on-ubuntu-boot](https://askubuntu.com/questions/1210411/failed-to-init-ppm-ppm-reset-failed-on-ubuntu-boot)大概就是安装一下驱动，但是我在实际操作的时候遇到了一些问题

```
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 nvidia-driver-470 : Depends: libnvidia-gl-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: nvidia-kernel-source-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-compute-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-extra-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: nvidia-compute-utils-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-decode-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-encode-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: nvidia-utils-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: xserver-xorg-video-nvidia-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-cfg1-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-ifr1-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Depends: libnvidia-fbc1-470 (= 470.82.00-0ubuntu0.20.04.1) but it is not going to be installed
                     Recommends: libnvidia-compute-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
                     Recommends: libnvidia-decode-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
                     Recommends: libnvidia-encode-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
                     Recommends: libnvidia-ifr1-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
                     Recommends: libnvidia-fbc1-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
                     Recommends: libnvidia-gl-470:i386 (= 470.82.00-0ubuntu0.20.04.1)
E: Unable to correct problems, you have held broken packages.
```

于是无法正常安装，现在还在探索解决方法。 不过我在尝试中发现另外一种解决方法，既然解决不了硬件的问题，那就解决产生问题的硬件。已知是nvidia的独显产生的bug，那么想办法将其屏蔽即可。通过安装tlp电源管理包后，tlp默认会屏蔽独显，使得这一bug得以暂时消失。输入

```bash
sudo apt install tlp tlp-rdw
sudo tlp start
```

即可。安装tlp后，无法开机的几率会减小一些，如果还是无法开机，可以通过重启、运行一次win10、通过resume模式打开等方式暂时修复。

### 安装ise

我在安装ise的过程中遇到了非常多的坑，但是之后找到了一篇博客，跟着这篇博客的流程进行安装，基本没有什么问题。
[https://antc2lt.medium.com/hello-fpga-nexys-3-setup-on-ubuntu-ff58e774566b](https://antc2lt.medium.com/hello-fpga-nexys-3-setup-on-ubuntu-ff58e774566b)
只有在安装ise时，会报错显示库缺失，对此，可以输入

```
sudo apt install libncurses5
```
