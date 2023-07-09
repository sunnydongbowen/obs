---
{"dg-publish":true,"dg-permalink":"使用yum安装docker","permalink":"/使用yum安装docker/","noteIcon":"","created":"2021-11-19","updated":""}
---

---
在线搭建 (客户端，服务端)，针对centos系统

```bash
wget -P /etc/yum.repos.d/  https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

```bash
yum -y install docker-ce docker-ce-cli containerd.io
systemctl enable docker
```