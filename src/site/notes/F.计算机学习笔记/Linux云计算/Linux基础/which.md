---
{"dg-publish":true,"dg-permalink":"which","permalink":"/which/","noteIcon":"","created":"2019-11-22","updated":""}
---


查看命令的目录，注意这个s权限比较特殊   [[F.计算机学习笔记/Linux云计算/Linux基础/文件rwx权限#5、 s权限\|文件rwx权限#5、 s权限]]
```bash
[root@os14 bowen]# which passwd
/usr/bin/passwd
[root@os14 bowen]# ls -lh /usr/bin/passwd
-rwsr-xr-x. 1 root root 33K Apr  7  2020 /usr/bin/passwd
```

查看useradd 命令目录
```bash
[root@os14 bowen]# which useradd
/usr/sbin/useradd
[root@os14 bowen]# ll /usr/sbin/useradd
-rwxr-xr-x. 1 root root 143424 Aug 13  2020 /usr/sbin/useradd
```

```ad-note
cd 命令是内置在内核里面的，这个命令比较特殊。但是我`which cd`是也能找到的。
```

## /bin 区别
---
![Pasted image 20230714202039.png](/img/user/Z.image/linux%E5%9F%BA%E7%A1%80/Pasted%20image%2020230714202039.png)