---
{"dg-publish":true,"dg-permalink":"ls命令","permalink":"/ls命令/","noteIcon":"","created":"2021-01-09","updated":""}
---


- 以人性化方式
```bash
[root@os53 ~]# ls -lh
total 129G
-rw-r--r--   1 root root  23G Aug 27 16:44  143-image.qcow2
-rw-r--r--   1 root root 302M Aug  4 14:05  4-virtio-win-0.1.141.iso
-rw-------.  1 root root  550 Aug 12 22:36  admin-openrc.sh
drwxr-xr-x   2 root root  136 May 12 10:33  amd64
```

和 ll 比起来，ls -lh 更人性化一些，文件大小信息看的更直观！
- ls命令（英文全拼：list）：用于查看目录下内容及目录和文件详细属性信息
- 命令格式：ls [-选项...] [参数...]
- 常用选项：
    - a 显示目录下所有内容，包含隐藏的内容
    - l 以长格式显示目录下的内容及详细属性
    - h 人性化显示目录下内容大小（kB、MB、GB）
    - d 仅显示目录本身而不显示目录下的内容
    - i 查看inode号（系统任何的文件或目录都有一个唯一的编号）
    - R：递归查看目录下所有内容（从头到尾）
- 按时间排序

```bash
ll -rlt
```

- ls与通配符的结合使用，在文件夹较多时会用到，看下面几个例子。匹配到why文件，并显示下面文件
```bash
# ll 目录会显示目录下的文件
[root@os55 ~]# ll w?y
total 851024
-rw-r--r-- 1 root root 602095648 May 20  2021  Active-HDL_11.1.261.7351_x64_main_setup.exe
-rw-r--r-- 1 root root  48004158 May 20  2021  Scientific_Toolworks_Understand.zip
-rw-r--r-- 1 root root 190290957 May 20  2021  样例系统源码.rar
```

```bash
[root@os55 ~]# ll z?.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc.tar
[root@os55 ~]# ll z?2.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc2.tar
[root@os55 ~]# ll z?*.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc2.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc.tar
[root@os55 ~]# ll z*.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc2.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc.tar
```

<span style="background:#d3f8b6">这个用法倒是挺好的。</span>
```bash
# 匹配到所有压缩包
[root@os55 ~]# ll *.tar
-rw-r--r--  1 root root   238580224 Dec  8 19:20 centos8.tar
-rw-r--r--  1 root root   946661376 Jun 28 17:54 centos-source-heat-engine.modified.tar
-rw-r--r--  1 root root  2154355712 Jul 21 17:04 centos-source-nova-compute.1.0.0.tar
-rw-------. 1 root root 10116872192 May  6  2021 images.tar
-rw-r--r--  1 root root   946661376 Dec 14 16:46 zc2.tar
-rw-r--r--  1 root root   946661376 Dec 14 16:46 zc.tar
```

```bash
ll w*
```

```bash
ll 2?2.txt
```

```bash
[root@os55 ~]# ll w?2.txt
ls: cannot access 'w?2.txt': No such file or directory
```

```bash
[root@os55 ~]# ll [w-z]*
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc2.tar
-rw-r--r-- 1 root root 946661376 Dec 14 16:46 zc.tar

why:
total 851024
-rw-r--r-- 1 root root 602095648 May 20  2021  Active-HDL_11.1.261.7351_x64_main_setup.exe
drwxr-xr-x 2 root root      4096 May 20  2021  alint-pro
-rw-r--r-- 1 root root 190290957 May 20  2021  样例系统源码.rar

zc:
total 10096
-rw-r--r--  1 root root 10330526 Aug 12 20:28 master
drwxr-xr-x 34 root root     4096 Aug 12 20:31 rocksdb-master
```