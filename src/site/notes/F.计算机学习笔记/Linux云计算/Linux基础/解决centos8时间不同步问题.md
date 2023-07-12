---
{"dg-publish":true,"dg-permalink":"解决centos8时间不同步问题","permalink":"/解决centos8时间不同步问题/","noteIcon":"","created":"2018-10-19","updated":""}
---


1、chrony服务配置文件
  > 这一步不改感觉也可以，直接执行步骤2
```bash
vim /etc/chrony.conf
# 注释掉不用的，把下面的加上
server 210.72.145.44 iburst
server ntp.aliyun.com iburst
```

2 、重启服务,同步时间
```bash
systemctl restart chronyd.service
chronyc sources -v
```

[CentOS 8时间同步_baozi_xiaoge的博客-CSDN博客_centos8时间同步](https://blog.csdn.net/baozi_xiaoge/article/details/103823996)

3、<font color="#ff0000">注意centos8是没有`ntp`服务的，网上的解决方法未必是对的！</font> [[F.计算机学习笔记/Linux云计算/Linux基础/修改系统时间\|修改系统时间]]
```bash
yum install chrony
systemctl restart chronyd.service
chronyc sources -v
```

![Pasted image 20230622161237.png](/img/user/Z.image/Linux/Pasted%20image%2020230622161237.png)
查看，时间改过来了！遇到问题不要嫌弃烦，要有点耐心去定位。还是去翻笔记找到，所以记笔记真的是很好的习惯！

