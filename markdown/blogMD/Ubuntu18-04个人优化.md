---
title: Ubuntu18.04个人优化
date: 2019-11-28 15:07:53
tags: Technology
---

Ubuntu18.04.2个人优化经验总结

惠普HP OMEN 15-ax239TX 暗影精灵 II 代Pro游戏本

I5-7300HQ

GTX1050M

Ubuntu18.04.2 [Torrent](http://releases.ubuntu.com/18.04.2/ubuntu-18.04.2-desktop-amd64.iso.torrent) [Directlink](http://releases.ubuntu.com/18.04.2/ubuntu-18.04.2-desktop-amd64.iso)

❗建议先看部分问题的解决方法

<!--more-->

# 替换默认源为国内源

管理员权限使用编辑器打开/etc/apt/sources.list

```bash
sudo vim /etc/apt/sources.list
```

> 如果你不知道如何使用vim，可以使用gedit
>
> ``` bash
> sudo gedit /etc/apt/sources.list
> ```

替换所有内容为如下所示

## 阿里源

```bash
# 阿里源
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

## 中科大源

```bash
# 中科大源
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial main main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
 
# 预发布软件源，不建议启用
# deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse
```

换完以后保存文件执行更新命令

```bash
sudo apt-get update
sudo apt-get upgrade
```

# 安装常用软件

## 视频播放器

想要找一款像Potplayer那样的播放器是不可能的，所以只能用mpv和vlc将就一下，smplayer也不错，就是界面过于古老

```bash
sudo apt-get install mpv vlc
sudo apt-get install smplayer
```

## VisualStudioCode

地表最强文本编辑器，可以去官网或者直接用自带的应用商店下载安装

[官网](https://code.visualstudio.com/Download)

## V2ray的安装与配置

[原文链接](https://www.wandouip.com/t5i197953/)

### **纯在线安装**

```bash
sudo su
bash <(curl -L -s https://install.direct/go.sh)
```

### **半在线安装，在Github上下载v2ray-linux-64.zip然后在文件目录下执行如下命令**

```bash
wget https://install.direct/go.shsudo bash go.sh --local ./v2ray-linux-64.zip
```

### **V2ray的配置**

我这里有Windows下V2rayN-Core自动生成的config.json所以配置变得很简单，只需要用它config替换/etc/v2ray/config.json就可以了

#### **替换config**

找到Windows下的config文件，在V2rayN-Core的根目录下

复制并替换掉/etc/v2ray/config.json

**重启服务**

```bash
sudo service v2ray restart
```

#### **设置系统代理**

打开系统的Proxy设置，选择Manual然后把config文件中的port和listen行填入对应的位置

举例：Sock5 address:127.0.0.0 port:1080

> listen对应的是address
>
> port对应的是port

#### 设置浏览器代理

确保浏览器正在使用系统代理

[![img](https://s2.ax1x.com/2019/11/28/Qi6bDg.gif)](https://s2.ax1x.com/2019/11/28/Qi6bDg.gif)

或者自己设置Sockv5的端口和地址，和设置系统代理填的一致

[![img](https://s2.ax1x.com/2019/11/28/QiccR0.gif)](https://s2.ax1x.com/2019/11/28/QiccR0.gif)

去Chrome或者Firefox扩展商店下载OmegaSwitch

导入设置OmegaSwitch的设置

[OmegaOptions.zip](https://www.lanzous.com/i7nk4qf)解压出OmegaOptions.bak然后按照下图操作

[![img](https://s2.ax1x.com/2019/11/28/Qiyqt1.gif)](https://s2.ax1x.com/2019/11/28/Qiyqt1.gif)

## Git

```bash
sudo apt-get install git
```

## vim

官方还不上vim，居心何在？？

```bash
sudo apt-get install vim
```

顺便提供基本操作：

[原文链接](https://www.cnblogs.com/harry335/p/5886405.html)

- `i` → *Insert* 模式，按 `ESC` 回到 *Normal* 模式.
- `x` → 删当前光标所在的一个字符。
- `:wq` → 存盘 + 退出 (`:w` 存盘, `:q` 退出)   （陈皓注：:w 后可以跟文件名）
- `dd` → 删除当前行，并把删除的行存到剪贴板里
- `p` → 粘贴剪贴板
- `hjkl` (推荐使用其移动光标，但不必需) →你也可以使用光标键 (←↓↑→). 注: `j` 就像下箭头。
- `:help <command>` → 显示相关命令的帮助。你也可以就输入 `:help` 而不跟命令。（注：退出帮助需要输入:q）

## 百度网盘

现在百度网盘有了Linux版，直接上[官网](https://pan.baidu.com/download)下载安装

## WPS Office

[官网](https://linux.wps.cn/)下载安装

## 网易云音乐

### ieaseMusic

网易云音乐第三方，做的还不错，个人认为界面有些花哨

[![Qi0ApD.gif](https://s2.ax1x.com/2019/11/28/Qi0ApD.gif)](https://s2.ax1x.com/2019/11/28/Qi0ApD.gif)

[项目地址](https://github.com/trazyn/ieaseMusic)

#### 安装

[下载deb文件](https://github.com/trazyn/ieaseMusic/releases/download/v1.3.4/ieaseMusic-1.3.4-linux-amd64.deb)

在文件目录打开终端执行以下命令

```bash
sudo dpkg -i ieaseMusic-1.3.4-linux-amd64.deb
```

### NetEase-MusicBox

高品质网易云音乐命令行版本，简洁优雅，丝般顺滑，基于Python编写

[![QiB5aq.md.gif](https://s2.ax1x.com/2019/11/28/QiB5aq.gif)](https://s2.ax1x.com/2019/11/28/QiB5aq.gif)

[项目地址](https://github.com/darknessomi/musicbox)

#### 安装

**注意：需要安装mpg123才能正常使用**

```bash
sudo apt-get install mpg123
```

**pip安装**

```bash
sudo susudo pip install NetEase-MusicBox
```

**如果没有安装pip就安装一个**

```bash
sudo apt-get install python-pip
```

**使用方法**

```bash
musicbox
```

### 网易云音乐官方

当然你也可以选择[官方客户端](https://lys1257.github.io/2019/11/28/Ubuntu18-04-2个人优化/d1.music.126.net/dmusic/netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb)

#### 高分屏下字体显示过小的问题

解决方案：

[原文链接](https://www.tuziang.com/combat/1120.html)

```bash
sudo gedit /usr/share/applications/netease-cloud-music.desktop
```

修改`Exec=`为如下所示

```bash
Exec=netease-cloud-music --force-device-scale-factor=1.25 %U
```

> 1.25是缩放比例，可根据自己的需要调整
>
> 调完之后网易云音乐的字体变大了，但是默认的窗口大小不变（因为网易云音乐锁死了默认的窗口大小），所以看起来就像是字挤在一起，放大窗口即可

## GoldenDict

最好用的本地词典，不接受反驳

```bash
sudo apt-get install goldendict
```

个人使用的词典：

链接：https://pan.baidu.com/s/1PWopLv3pATWERYFCZ2JXnw
提取码：kf6a

## QQLinux版

TX隔了这么久终于又发布了linux版的QQ，虽然目前的功能不是很完善，但我觉得有必要放上来

[官网链接](https://im.qq.com/linuxqq/index.html)

## Deepin软件安装

[项目地址](https://github.com/Jactor-Sue/Deepin-Apps-Installation)

### 安装

**克隆仓库到本地**

```bash
git clone https://github.com/Jactor-Sue/Deepin-Apps-Installation.git
```

**安装deepin-wine**

```bash
chmod +x ./install-deepin-wine.sh && ./install-deepin-wine.sh
```

**安装Deepin移植的软件**

`deepin-apps`文件夹下有一些常用的软件，选择需要的软件安装，或直接在文件浏览器中双击安装包安装

```bash
cd ./deepin-appssudo dpkg -i xxx.deb
```

### 卸载

**卸载apps**

```bash
sudo dpkg -P xxx 
#xxx为安装时的包名
```

**卸载deepin-wine**

```bash
chmod+x ./uninstall-deepin-wine.sh && ./uninstall-deepin-wine.sh
```

> **注意：** 卸载`deepin-wine`之后已经安装的apps会由于依赖问题也被卸载
>
> 这个容器里的迅雷极速版下载东西虽然没有问题，但是字体全都是框框，暂时没有解决（懒

#### 我遇到的问题和解决方法

> 字体问题

QQ安装完以后在我的机器上没法正常显示字体，全都是框框

我查了查发现是simsun这个字体没有安装，安装完以后显示正常，但是`simsun`字体过于丑陋，于是我就把`Microsoft-Yahei`的字体属性改成了`simsun`并安装，QQ的字体就变成了`Microsoft-Yahei`

这里提供一个我修改好的字体文件

https://www.lanzous.com/i7nj0sh

##### 渲染问题

由于我的屏幕属于高分屏，而Wine默认的应用DPI是96，所以显示的非常糟糕，只需要调整应用的Wine配置就可以了

这是官方的解决方法：

**高分屏调整DPI**

`deepin-wine`打包的软件默认96 dpi，在高分屏下字体和窗口会很小

**解决方案**

打开Wine configuration界面，以微信为例

```bash
WINEPREFIX=~/Deepin-WeChat/ deepin-wine winecfg
```

在Graphics标签下修改dpi，我设置的120(1.25倍)

**这个方法对我不适用，于是我就换了一个方法**

[原文链接](https://www.linux265.com/news/1111.html)

**步骤如下：**

1，先退出deepin-tim或deepin-qq，否则会提示错误。

2，运行`env WINEPREFIX="$HOME/.deepinwine/Deepin-TIM" winecfg`（如果是修改QQ界面字体大小，就把Deepin-TIM改成Deepin-QQ），然后将屏幕分辨率拖放到合适的大小，如下图所示：

[![QiuyCV.md.png](https://s2.ax1x.com/2019/11/28/QiuyCV.md.png)](https://imgchr.com/i/QiuyCV)

## 常用设置

### 设置快捷键

打开keyboard设置快捷键

快捷键的工作方式是通过按键在终端执行特定的命令

比如要想用Win+E打开默认的文件管理器（nautilus）可以把执行的命令设置成nautilus然后录入快捷键

命令：

```bash
nautilus
```

如果想要以sudo权限打开，只需要在nautilus前面加上sudo就可以了

```bash
sudo nautilus
```

### 添加右键以管理员权限打开文件夹选项

安装插件

```bash
sudo apt install nautilus-admin
```

重启nautilus

```bash
nautilus -q
```

### Ubuntu 18.04 设置开机自动执行脚本

[原文链接](https://blog.csdn.net/github_38336924/article/details/98183253)

- Ubuntu18.04 默认是没有 /etc/rc.local 这个文件的，需要自己创建
- systemd 默认读取 /etc/systemd/system  下的配置文件，该目录下的文件会链接/lib/systemd/system/下的文件。执行 ls /lib/systemd/system  你可以看到有很多启动脚本，其中就有我们需要的 rc.local.service
- 查看rc.local.service文件内容

```bash
#  SPDX-License-Identifier: LGPL-2.1+
#
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# This unit gets pulled automatically into multi-user.target by
# systemd-rc-local-generator if /etc/rc.local is executable.
[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no
```

- 一般正常的启动文件主要分成三部分
  `[Unit]` 段: 启动顺序与依赖关系
  `[Service]` 段: 启动行为,如何启动，启动类型
  `[Install]` 段: 定义如何安装这个配置文件，即怎样做到开机启动
- 可以看出，rc.local.service 它少了 Install 段，也就没有定义如何做到开机启动，所以显然这样配置是无效的。  因此我们就需要在后面帮他加上 [Install]  段，可以发现rc.local.service是rc-local.service文件的链接文件，所以我们**只需要修改**rc-local.service文件即可：

- ```bash
  [Install]  
  WantedBy=multi-user.target  
  Alias=rc-local.service
  ```

#### 操作步骤

- 在`/lib/systemd/system/rc-local.service` 文件中添加如下代码：

  ```bash
  [Install]  
  WantedBy=multi-user.target  
  Alias=rc-local.service
  ```

* 在`/etc/`目录下面创建`rc.local`文件，赋予执行权限

  ~~~ bash
  root@dyjc-bmg:/home/vagrant# touch /etc/rc.local
  root@dyjc-bmg:/home/vagrant# chmod +x /etc/rc.local
  ~~~

* `/etc/rc.local` 文件添加如下内容：

  ~~~ bash
  #!/bin/sh -e
  #
  # rc.local
  #
  # This script is executed at the end of each multiuser runlevel.
  # Make sure that the script will "exit 0" on success or any other
  # value on error.
  #
  # In order to enable or disable this script just change the execution
  # bits.
  #
  # By default this script does nothing.
    
  exit 0
  ~~~

  

* systemd 默认读取 `/etc/systemd/system` 下的配置文件，将`/lib/systemd/system/rc.local.service` 链接到`/etc/systemd/system`目录

  ~~~ bash
  root@dyjc-bmg:/home/vagrant# ln -s /lib/systemd/system/rc.local.service /etc/systemd/system/
  ~~~

**注意:** 一定要将命令添加在 `exit 0`之前

**注意:** 一定要将命令添加在 `exit 0`之前

### 关闭笔记本自带键盘

[原文链接](https://www.cnblogs.com/xia-Autumn/p/6698725.html)

1. 使用`xinput list` 找到笔记本键盘的ID 可以看到，在这台机器上，`AT Translated Set 2 Keyboard`项的ID为15

2. 使用`xinput set-prop 15 "Device Enabled" 0`来禁用笔记本键盘。如果要重新启用它，则将0更改为1即可

   ```bash
   xxx@X550VX:~$ xinput list
   ⎡ Virtual core pointer                        id=2    [master pointer  (3)]
   ⎜   ↳ Virtual core XTEST pointer                  id=4    [slave  pointer  (2)]
   ⎜   ↳ RAPOO Rapoo 2.4G Wireless Device            id=11    [slave  pointer  (2)]
   ⎜   ↳ SIGMACHIP USB Keyboard                      id=13    [slave  pointer  (2)]
   ⎜   ↳ FocalTechPS/2 FocalTech FocalTech Touchpad  id=16    [slave  pointer  (2)]
   ⎣ Virtual core keyboard                       　　 id=3    [master keyboard (2)]
       ↳ Virtual core XTEST keyboard                 id=5    [slave  keyboard (3)]
       ↳ Power Button                                id=6    [slave  keyboard (3)]
       ↳ Video Bus                                   id=7    [slave  keyboard (3)]
       ↳ Video Bus                                   id=8    [slave  keyboard (3)]
       ↳ Sleep Button                                id=9    [slave  keyboard (3)]
       ↳ USB2.0 VGA UVC WebCam                       id=10    [slave  keyboard (3)]
       ↳ SIGMACHIP USB Keyboard                      id=12    [slave  keyboard (3)]
       ↳ Asus WMI hotkeys                            id=14    [slave  keyboard (3)]
       ↳ AT Translated Set 2 keyboard                id=15    [slave  keyboard (3)]
   xxx@X550VX:~$ xinput set-prop 15 "Device Enabled" 0
   xxx@X550VX:~$ xinput set-prop 15 "Device Enabled" 1
   xxx@X550VX:~$ xinput set-prop 15 "Device Enabled" 0
   xxx@X550VX:~$
   ```

# 配置中文输入法

我用的是系统自带的Ibus，只需要安装完整的语言支持，然后在设置里面选择中文输入法就可以了

以下是详细信息

[原文链接](https://www.cnblogs.com/YMaster/p/8967233.html)

## 在Ubuntu18.04中使用自带中文输入法

ubuntu 在最新的版本中已经可以不用用户自己单独去下载中文输入法使用了，本次使用为 ubuntu18.04LTS版本(登陆是界面选择的是ubuntu on wayland)，设置方式非常简单

1、打开设置，不知道的请点击右上角的工具栏即可看到。
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428135813506-1891890434.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428135813506-1891890434.png)

2、找到设置中语言项，点击语言安装管理，安装中文语言后选择输入方式。
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134309719-98960050.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134309719-98960050.png)
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134533018-1710981457.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134533018-1710981457.png)

点击关闭，然后添加输入语言，在其中找到中文拼音添加即可
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134603731-1125922656.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134603731-1125922656.png)
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134635766-2121728441.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134635766-2121728441.png)
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134747656-874779816.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134747656-874779816.png)
 [![img](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134852118-2061594231.png)](https://images2018.cnblogs.com/blog/1078966/201804/1078966-20180428134852118-2061594231.png)

可以看到中文输入法已经存在了，点击选择即可使用了

## 搜狗拼音解决方案

[原文链接](https://blog.csdn.net/fx_yzjy101/article/details/80243710)

我个人不推荐使用搜狗，容易出问题，不过还是把它贴出来比较好

首先安装fcitx

1. 检测是否安装fcitx
   首先检测是否有fcitx，因为搜狗拼音依赖fcitx

> fcitx
> 提示：
> 程序“fcitx”尚未安装。 您可以使用以下命令安装：
>
> ```bash
> sudo apt-get install fcitx-bin
> ```

2. 安装fcitx

```bash
sudo apt-get install fcitx-bin
```

相关的依赖库和框架都会自动安装上。

[![Qis6G6.png](https://s2.ax1x.com/2019/11/28/Qis6G6.png)](https://s2.ax1x.com/2019/11/28/Qis6G6.png)

```bash
sudo apt-get install fcitx-table
```

安装输入法

[![QiscRK.png](https://s2.ax1x.com/2019/11/28/QiscRK.png)](https://s2.ax1x.com/2019/11/28/QiscRK.png)

3. 配置fcitx
   默认iBus（非常难用），前面我们说过了，安装完fcixt后你尽可以如意地在 键盘输入方式系统 处把它替换为fcitx（如下图）。然后重启Ubuntu。

   [![QisyPx.png](https://s2.ax1x.com/2019/11/28/QisyPx.png)](https://s2.ax1x.com/2019/11/28/QisyPx.png)

4. 选择需要的输入法
   点击Ubuntu右上角顶栏的小键盘图标中打开，配置，如下图：

   [![QisrI1.png](https://s2.ax1x.com/2019/11/28/QisrI1.png)](https://s2.ax1x.com/2019/11/28/QisrI1.png)

配置之后，就可以使用拼音输入了。

[![QisDaR.png](https://s2.ax1x.com/2019/11/28/QisDaR.png)](https://s2.ax1x.com/2019/11/28/QisDaR.png)

5. 安装搜狗拼音
   访问搜狗输入法For Linux
   https://pinyin.sogou.com/linux/?r=pinyin
   点击立即下载64bit，下载安装文件。

   [![QisRMD.png](https://s2.ax1x.com/2019/11/28/QisRMD.png)](https://s2.ax1x.com/2019/11/28/QisRMD.png)

下载后，双击下载的文件。

[![QisWse.png](https://s2.ax1x.com/2019/11/28/QisWse.png)](https://s2.ax1x.com/2019/11/28/QisWse.png)

点击安装，输入密码，就可以安装了。安装完成重启Ubuntu。

[![QisfqH.png](https://s2.ax1x.com/2019/11/28/QisfqH.png)](https://s2.ax1x.com/2019/11/28/QisfqH.png)

重启后，点击右上角小键盘-设置，调整一下输入法顺序。熟悉的输入感觉就来了。

[![Qis4Zd.png](https://s2.ax1x.com/2019/11/28/Qis4Zd.png)](https://s2.ax1x.com/2019/11/28/Qis4Zd.png)

更改设置，点击输入操作条上的扳手按钮，可以设置皮肤，设置熟悉的习惯，还可以登录个人中心，同步个人词库。

[![Qis5dA.png](https://s2.ax1x.com/2019/11/28/Qis5dA.png)](https://s2.ax1x.com/2019/11/28/Qis5dA.png)

# 安装NVIDIA显卡驱动

[原文链接](https://blog.csdn.net/luteresa/article/details/79555356)

**安装之前进入BIOS下先把UEFI安全启动关掉**

1. 禁用Ubuntu默认显卡（集显）驱动

   ~~~ bash
   sudo chmod 666 /etc/modprobe.d/blacklist.conf
   sudo vim /etc/modprobe.d/blacklist.conf
   ~~~

   在文件最末尾添加如下：

   ```bash
   blacklist vga16fb
   blacklist nouveau
   blacklist rivafb
   blacklist rivatv
   blacklist nvidiafb
   ```

   更新内核

   ~~~ bash
   sudo update-initramfs -u
   ~~~

   重启

   查看驱动，无任何打印则说明已经被屏蔽掉

   ~~~ bash
   lsmod | grep nouveau
   ~~~

   ~~~ bash
   sudo add-apt-repository ppa:graphics-drivers/ppa
   sudo apt-get update
   ~~~

2. 

3. 寻找合适驱动版本：

   ``` bash
   ubuntu-drivers devices
   ```

   推荐使用axel安装推荐版本（recommend）

   ``` bash
   sudo apt-fast install nvidia-driver-xxx
   ```

   当然你也可以直接用

   ``` bash
   sudo apt-get install nvidia-driver-xxx
   ```

4. 安装完之后重启

   ``` bash
   sudo reboot
   ```

5. 查看驱动安装状态：

   ``` bash
   sudo nvidia-smi
   ```

   ![img](https://s2.ax1x.com/2019/11/28/QigiSP.png)

   打开nvidia设置

   ``` bash
   sudo nvidia-settings
   ```

   [![img](https://s2.ax1x.com/2019/11/28/QigFQf.png)](https://s2.ax1x.com/2019/11/28/QigFQf.png)

# 部分问题的解决方法

## 解决ppa.launchpad.net下载速度过慢问题

[原文链接](https://learnku.com/articles/33436?order_by=vote_count&)

**安装axel**

```bash
sudo apt-get install axel
sudo axel -o /usr/bin/apt-fast http://www.mattparnell.com/linux/apt-fast/apt-fast.sh
sudo chmod +x /usr/bin/apt-fast
```

**使用**

将apt换成apt-fast即可

```bash
sudo apt-fast install xxx
```

## 解决Ubuntu屏幕自动旋转问题

```bash
sudo xrandr -o normal
```

然后等恢复正常以后关闭屏幕自动旋转

# Gnome桌面环境配置

## 基本配置

1. **安装gnome-tweak-tool**

   这个工具主要是用来调整字体大小和主题的

   ```bash
   sudo apt install gnome-tweak-tool
   ```

   用su的权限安装chrome-gnome-shell

   ``` bash
   sudo su
   sudo apt-get install chrome-gnome-shell
   ```

2. **安装GNOME Shell integration扩展插件，Firefox和Chrome都有**，安装完之后就可以点开管理插件了

## GNOME扩展推荐

#### 部分扩展整合包

```bash
sudo apt-get install gnome-shell-extensions
```

安装完以后可以在Tweak里面的Extension选项中看到多了很多的扩展

#### **[OpenWeather**](https://extensions.gnome.org/extension/750/openweather/)

用于显示天气，还不错

[![QiuScF.jpg](https://s2.ax1x.com/2019/11/28/QiuScF.jpg)](https://s2.ax1x.com/2019/11/28/QiuScF.jpg)

#### **[Drop down terminal**](https://extensions.gnome.org/extension/442/drop-down-terminal/)

下滑式的Shell

[![QiuY38.md.png](https://s2.ax1x.com/2019/11/28/QiuY38.md.png)](https://imgchr.com/i/QiuY38)

#### [TopIcon Plus](https://extensions.gnome.org/extension/1031/topicons/)

解决Wine System Tray一直显示在非通知区的问题

[![Qinz1U.png](https://s2.ax1x.com/2019/11/28/Qinz1U.png)](https://s2.ax1x.com/2019/11/28/Qinz1U.png)

#### [Dash to Panel](https://extensions.gnome.org/extension/1160/dash-to-panel/)

把你的任务栏调整成Windows的样式

[![QinjhV.png](https://s2.ax1x.com/2019/11/28/QinjhV.png)](https://s2.ax1x.com/2019/11/28/QinjhV.png)

## GNOME主题推荐

**注意：**

- **Ubuntu18.04默认使用的是Gnome3，所以只能用GTK3的主题，不能用GTK2**
- **在使用主题前请开启Extension里面的UserTheme**

#### OCS-URL

在安装主题之前强烈推荐安装ocs-url，安装之后就可以可以直接在网页中安装主题和Shell主题，免去了手动安装的麻烦

[ocs-url.deb](https://dllb2.pling.com/api/files/download/id/1530774600/s/527d04e6722ce114b290fd4c4d90bb11671e3895cb62081cdb9a6e3bde251e8068379c77defdeaf6306d5076d0b4d39f6066ee14de8e57ce59a1a5fb07440e2f/t/1574920436/c/527d04e6722ce114b290fd4c4d90bb11671e3895cb62081cdb9a6e3bde251e8068379c77defdeaf6306d5076d0b4d39f6066ee14de8e57ce59a1a5fb07440e2f/lt/download/ocs-url_3.1.0-0ubuntu1_amd64.deb)

安装了以后就可以在主题界面点击Install按钮，选择自己要安装的版本然后选择用ocs-url打开ocs链接

[![Image](https://s2.ax1x.com/2019/11/28/QikJUO.gif)](https://s2.ax1x.com/2019/11/28/QikJUO.gif)

> 我是在Windows下做的演示，如果你已经安装了ocs-url，你看到的就是选择用ocs-url打开的界面

#### [Qogir theme](https://www.gnome-look.org/p/1230631/)

[![img](https://s2.ax1x.com/2019/11/28/QiV6IK.png)](https://s2.ax1x.com/2019/11/28/QiV6IK.png)

#### [Arc-Darkest Complete Desktop](https://www.gnome-look.org/p/1317409/)

[![img](https://s2.ax1x.com/2019/11/28/QiVa24.png)](https://s2.ax1x.com/2019/11/28/QiVa24.png)

## GRUB主题推荐

#### [Atomic GRUB](https://www.gnome-look.org/p/1200710/)

[![img](https://s2.ax1x.com/2019/11/28/QiVDq1.gif)](https://s2.ax1x.com/2019/11/28/QiVDq1.gif)

#### [Aurora Penguinis](https://www.gnome-look.org/p/1009533/)

[![img](https://s2.ax1x.com/2019/11/28/QiVBrR.png)](https://s2.ax1x.com/2019/11/28/QiVBrR.png)

## GnomeShell主题推荐

#### [Copernico Theme](https://www.gnome-look.org/p/1013056/)

[![img](https://s2.ax1x.com/2019/11/28/QiV1rn.png)](https://s2.ax1x.com/2019/11/28/QiV1rn.png)

#### [ChromeOS shell theme](https://www.gnome-look.org/p/1333760/)

[![img](https://s2.ax1x.com/2019/11/28/QiZ8QH.jpg)](https://s2.ax1x.com/2019/11/28/QiZ8QH.jpg)

## 图标推荐

#### [Qogir icon theme](https://www.gnome-look.org/s/Gnome/p/1296407)

[![img](https://s2.ax1x.com/2019/11/28/QiVJaV.png)](https://s2.ax1x.com/2019/11/28/QiVJaV.png)

#### [Papirus](https://www.gnome-look.org/s/Gnome/p/1166289)

[![img](https://s2.ax1x.com/2019/11/28/QiVGV0.png)](https://s2.ax1x.com/2019/11/28/QiVGV0.png)

#### [Tela-icon-theme](https://www.gnome-look.org/s/Gnome/p/1279924)

[![img](https://s2.ax1x.com/2019/11/28/QiVNPU.png)](https://s2.ax1x.com/2019/11/28/QiVNPU.png)

**本人已经抛弃Ubuntu，转用Manjaro KDE Plasma 19.0.2**

**2020年4月26日**