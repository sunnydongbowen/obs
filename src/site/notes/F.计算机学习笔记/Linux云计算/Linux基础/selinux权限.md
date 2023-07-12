---
{"dg-publish":true,"dg-permalink":"selinux权限","permalink":"/selinux权限/","noteIcon":"","created":"2019-11-22","updated":""}
---

# 1 查看selinux权限

```bash
getenforce        # permissive是关闭
sestatus
[root@os55 ~]# sestatus
SELinux status:                 disabled
```

# 2 修改selinux权限

1、临时修改
```bash
setenforce 0     ##设置SELinux 成为permissive模式
```

2、永久修改
- 修改/etc/selinux/config 文件
- 将SELINUX=enforcing改为SELINUX=disabled
- 重启机器即可
![Pasted image 20230712101607.png](/img/user/Pasted%20image%2020230712101607.png)

```bash
sed -i '/^SELINUX=/c SELINUX=disabled' /etc/selinux/config
```