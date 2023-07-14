---
{"dg-publish":true,"dg-permalink":"find用法","permalink":"/find用法/","noteIcon":"","created":"2021-01-09","updated":""}
---


# 1、报错解决方法
---
centos8.3 2011 装完系统之后，执行find 命令。报错
```bash
find: ‘/run/user/1000/gvfs’: Permission denie
```

解决方法
```bash
umount /run/user/1000/gvfs
rm -rf /run/user/1000/gvfs
```

补充一次删除所有目录的目标文件或文件
```bash
find / -name ***|xargs rm -rf     //***为你要删除的文件或文件夹
```

# 2、补充find 用法
---
```bash
# 一般记住这个就可以了。后面要记住的可能就是查看较大文件的那个命令。
find / -name getcpu.py
find /path  -name ....
```

```bash
find  ./ -name “*.txt” | xargs rm    (删除当前目录下所有以txt结尾的文件)**
find   /home   -size   +512k   +2M   查大于512k的文件
find   /home   -size   -512k   -2M   查小于512k的文件
find   /home   -links   +2           查硬连接数大于2的文件或目录
find   /home   -perm   0700          查权限为700的文件或目录
find    /   -amin    -10       # 查找在系统中最后10分钟访问的文件
find    /   -atime   -2        # 查找在系统中最后48小时访问的文件
find    /   -empty             # 查找在系统中为空的文件或者文件夹
find    /   -group   cat       # 查找在系统中属于 groupcat的文件
find    /   -mmin   -5         # 查找在系统中最后5分钟里修改过的文件
find    /   -mtime   -1        #查找在系统中最后24小时里修改过的文件
find    /   -nouser            #查找在系统中属于作废用户的文件
find    /   -user    fred      #查找在系统中属于FRED这个用户的文件
```

```bash
# 与通配符结合使用
[root@localhost iso]# find  ./ -name "*.raw"
./win10.raw
./centos7.9.raw

[root@localhost iso]# find  / -name "*.raw"
/home/iso/win10.raw
/home/iso/centos7.9.raw
```