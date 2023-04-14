---
title: dd命令写入镜像文件到U盘
date: 2023-03-28 18:41:12 +0800
categories: [ubuntu, dd_command]
tags: [dd, iso]     # TAG names should always be lowercase
toc: true
math: true
mermaid: true
pin: false  # pin one or more posts to the top of the home page and the fixed posts are sorted in reverse order according to their release date

---

linux下使用dd命令写入镜像文件到U盘的方法：
1. 使用 `df -h`，查看U盘所代表的磁盘标符，比如盘符是 `/dev/sdb1`  

2. 将U盘的所有分区去挂载掉  
   `sudo umount /dev/sdb1`  

3. 使用dd命令将镜像写入刚才找到的分区，注意：不用写分区号。  
   `sudo dd if=/home/jack/ubuntu.16.04.iso of=/dev/sdb bs=4M`  

4. 可以在另外一个终端观察运行情况。   
   `sudo watch kill -USR1 $(pgrep ^dd)`  
解释一下：watch观察命令的运行，kill命令发送一段信号，-USR1是dd专用的信号，它接收到该信号，就会显示刻录的进度  

5. 当刻录结束后，运行  
   `sync`  
       该命令是检查一下，刻录是否运行完毕，当sync结束后，就可以安全的拔出u盘  

