---
{"dg-publish":true,"dg-permalink":" ","permalink":"/ /","noteIcon":"","created":"2022-11-29","updated":""}
---


## 文件权限
---
- 去读写权限
```bash
[cloud@os14 ~]$ touch 01.py
[cloud@os14 ~]$ ll
total 0
-rw-rw-r--. 1 cloud cloud 0 Dec 27 18:27 01.py

[cloud@os14 ~]$ vi 01.py
[cloud@os14 ~]$ ll
total 4
-rw-rw-r--. 1 cloud cloud 4 Dec 27 18:27 01.py

[cloud@os14 ~]$ chmod -rw 01.py
[cloud@os14 ~]$ vi 01.py
[cloud@os14 ~]$ cat 01.py
cat: 01.py: Permission denied
[cloud@os14 ~]$ ll
total 4
----------. 1 cloud cloud 4 Dec 27 18:27 01.py
```

- 加读写权限
```bash
[cloud@os14 ~]$ chmod +r 01.py
[cloud@os14 ~]$ chmod +w 01.py
                chmod +rw 01.py
```

- 加执行权限
```bash
chmod +x 01.py
```

## 目录权限
---
目录的可执行权限很重要，如果没有可执行权限，根本没有进不去目录，ls也不行，默认的权限

```bash
drwxrwxr-x. 2 cloud cloud  6 Dec 27 22:58 python
```

- ls是需要可读权限的
- cd 是需要执行权限的
- touch 是需要写权限的