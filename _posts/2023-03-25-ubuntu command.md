---
title: ubuntu command
date: 2023-03-25 23:10:12 +0800
categories: [ubuntu, ubuntu_command]
tags: [ubuntu]     # TAG names should always be lowercase
toc: true
math: true
mermaid: true
pin: false  # pin one or more posts to the top of the home page and the fixed posts are sorted in reverse order according to their release date
---

Abstract: This post will instruct you how to use every command for [**ubuntu system**], including files managment, nautilus, system managment, apt command, system update, and so on.&emsp;&emsp;&emsp;&emsp;&emsp;

## 文件/文件夹管理

`ls` 列出当前目录文件（不包括隐含文件）  
`ls -a` 列出当前目录文件（包括隐含文件）  
`ls -l` 列出当前目录下文件的详细信息

`cd ..` 回当前目录的上一级目录  
`cd -` 回上一次所在的目录  
`cd ~ 或 cd` 回当前用户的宿主目录  

`mkdir 目录名` 创建一个目录  
`rmdir 空目录名` 删除一个空目录  
`rm 文件名 文件名` 删除一个文件或多个文件  
`rm -rf 非空目录名` 删除一个非空目录下的一切

`mv 路经/文件` /经/文件移动相对路经下的文件到绝对路经下  
`mv 文件名 新名称` 在当前目录下改名  
`find 路经 -name “字符串”` 查找路经所在范围内满足字符串匹配的文件和目录

## Nautilus

`Ctrl+h` 显示隐藏文件  
`Ctrl+l` 显示地址栏

## 系统管理

`fdisk fdisk -l` 查看系统分区信息  
`fdisk fdisk /dev/sdb` 为一块新的SCSI硬盘进行分区  
`chown chown root /home` 把/home的属主改成root用户  
`chgrp chgrp root /home` 把/home的属组改成root组

`Useradd` 创建一个新的用户  
`Groupadd 组名` 创建一个新的组  
`Passwd 用户名` 为用户创建密码  
`Passwd -d用户名` 删除用户密码也能登陆  
`Passwd -S用户名` 查询账号密码  
`Usermod -l 新用户名 老用户名` 为用户改名  
`Userdel–r 用户名` 删除用户一切

`service [servicename] start/stop/restart` 系统服务控制操作  
`/etc/init.d/[servicename] start/stop/restart` 系统服务控制操作

`cat /etc/issue` 查看ubuntu版本  
`lsusb` 查看usb设备  
`sudo ethtool eth0` 查看网卡状态  
`cat /proc/cpuinfo` 查看cpu信息  
`lshw` 查看当前硬件信息  
`sudo fdisk -l` 查看磁盘信息  
`df -h` 查看硬盘剩余空间  
`free -m` 查看当前的内存使用情况  
`ps -A` 查看当前有哪些进程  
`kill 进程号`(就是ps -A中的第一列的数字)或者 `killall 进程名`( 杀死一个进程)  
`kill -9 进程号` 强制杀死一个进程

`reboot Init 6` 重启LINUX系统  
`Halt Init 0 Shutdown –h now` 关闭LINUX系统

### 解决内核版本问题
`uname -a` 查看内核版本  
`dpkg --get-selections|grep linux` 查看目前系统中存在的内核版本  
`sudo apt-get remove linux-image-x.x.x-xx-generic` 删除多余的内核   
`sudo dpkg -P linux-image-x.x.x-xx-generic` 删除那些是deinstall的内核版本  
`sudo apt-cache search linux-image` 查看可更新的内核  
执行命令`sudo apt-get install linux-image-extra-X.XX.0-85-generic` 安装  
执行命令`dpkg -l | grep 3.13.0-85-generic` 查看是否安装成功  

- `sudo vi /etc/default/grub` 用编辑器打开 grub 配置文件，修改引导文件  
- 找到 `GRUB_DEFAULT=0`, 修改为
`GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 3.13.0-85-generic"`
具体看自己下载什么版本修改  
- 保存退出，然后执行`sudo update-grub`命令更新 Grub 引导  
- 更新完成后重启系统`sudo reboot`  
- `sudo apt-get install linux-headers-$(uname -r)`安装linux-headers

## apt & dpkg 命令

`apt-cache search package` 搜索包  
`apt-cache show package` 获取包的相关信息，如说明、大小、版本等  
`sudo apt-get install package` 安装包  
`sudo apt-get install package - - reinstall` 重新安装包  
`sudo apt-get -f install` 修复安装”-f = –fix-missing”  
`sudo apt-get remove package` 删除包  
`sudo apt-get remove package - - purge` 删除包，包括删除配置文件等  
`sudo apt-get update` 更新源  
`sudo apt-get upgrade` 更新已安装的包  
`sudo apt-get dist-upgrade` 升级系统  
`sudo apt-get dselect-upgrade` 使用 dselect 升级  
`apt-cache depends package` 了解使用依赖  
`apt-cache rdepends package` 是查看该包被哪些包依赖  
`sudo apt-get build-dep package` 安装相关的编译环境  
`apt-get source package` 下载该包的源代码  
`sudo apt-get clean && sudo apt-get autoclean` 清理无用的包  
`sudo apt-get check` 检查是否有损坏的依赖  
`sudo apt-get clean` 清理所有软件缓存（即缓存在/var/cache/apt/archives目录里的deb包）

`sudo dpkg -r name` 只是卸载，保留配置  
`sudo dpkg --remove  name` 只是卸载，保留配置  
`sudo dpkg -r name` 彻底清除，包括配置  
`sudo dpkg --purge  name` 彻底清除，包括配置

## 系统升级
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

清除所有删除包的残余配置文件
`dpkg -l |grep ^rc|awk ‘{print $2}’ |tr ["\n"] [" “]|sudo xargs dpkg -P -`

编译时缺少h文件的自动处理
`sudo auto-apt run ./configure`

查看安装软件时下载包的临时存放目录
`ls /var/cache/apt/archives`

备份当前系统安装的所有包的列表
`dpkg –get-selections | grep -v deinstall > ~/somefile`

从上面备份的安装包的列表文件恢复所有包
`dpkg –set-selections < ~/somefile sudo dselect`

`sudo apt-get autoclean` 清理旧版本的软件缓存  
`sudo apt-get clean` 清理所有软件缓存  
`sudo apt-get autoremove` 删除系统不再使用的孤立软件  
`apt-get -qq –print-uris install ssh | cut -d\’ -f2` 查看包在服务器上面的地址

## 系统

`uname -a` 查看内核  
`cat /etc/issue` 查看Ubuntu版本  
`lsmod` 查看内核加载的模块  
`lspci` 查看PCI设备  
`lsusb` 查看USB设备  
`sudo ethtool eth0` 查看网卡状态  
`cat /proc/cpuinfo` 查看CPU信息  
`lshw` 显示当前硬件信息

## 打包/解压

`tar -c` 创建包 `–x` 释放包 `-v` 显示命令过程 `–z` 代表压缩包  
`tar –cvf benet.tar /home/benet` 把/home/benet目录打包  
`tar –zcvf benet.tar.gz /mnt` 把目录打包并压缩  
`tar –zxvf benet.tar.gz` 压缩包的文件解压恢复  
`tar –jxvf benet.tar.bz2` 解压缩

## make编译

`make` 编译  
`make install` 安装编译好的源码包

## 硬盘

`sudo fdisk -l` 查看硬盘的分区  
`sudo hdparm -i /dev/hda` 查看IDE硬盘信息  
`sudo hdparm -I /dev/sda` 查看STAT硬盘信息  
`df -h`,`df -H` 查看硬盘剩余空间  
`du -hs 目录名` 查看目录占用空间  
`sync fuser -km /media/usbdisk` 优盘没法卸载

## 内存

`free -m` 查看当前的内存使用情况

## 进程

`ps -A` 查看当前有哪些进程  
`kill 进程号(就是ps -A中的第一列的数字) 或者 killall 进程名` 中止一个进程  
`kill -9 进程号 或者 killall -9 进程名` 强制中止一个进程(在上面进程中止不成功的时候使用)  
`top` 查看当前进程的实时状况


