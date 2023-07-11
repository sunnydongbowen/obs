---
{"dg-publish":true,"dg-permalink":"centos8网络管理","permalink":"/centos8网络管理/","noteIcon":"","created":"2022-01-09","updated":""}
---


# 1、安装network-scripts
---
```bash
yum install network-scripts
service network restart
```
centos8中，network.service 是没有的，如果想用，要手动装一下，方便管理网络。当然，nmcli也很好用的! 记不住命令去翻一下就好了。

# 2、nmtui
---
配置网络，可使用nmtui。例如下面，具体怎么配置，百度参考一下细节的配置，比如ipv4和v6，子网掩码，网关和默认路由等。尽量不要配错，之前使用nmtui配置，导致vmware虚拟机我始终连不上，最后改成自动获取重启网络解决。真用还是得写死在配置文件里。慎用这个方法改ip和禁用，不然就连不上了！

![https://cdn.nlark.com/yuque/0/2021/png/812311/1618235608473-79c38125-7c43-4248-8485-33f4f76811a4.png](https://cdn.nlark.com/yuque/0/2021/png/812311/1618235608473-79c38125-7c43-4248-8485-33f4f76811a4.png)

[Linux安全之SSH 密钥创建及密钥登录_呐喊的专栏-CSDN博客_ssh密钥登录](https://blog.csdn.net/nahancy/article/details/79059135)
网上有nmcli方法，不习惯用，安装network-scripts,或者使用nmtui吧。不过使用nmcli做bond很方便！使用nmtui时没有办法重启网卡，重启的时候直接断掉没法启动了。

# 3、nmcli
---
```bash
nmcli c reload ens160
nmcli c up ethX
```
> 常用的命令网上去查一下就好，不需要记忆

# 4、vmware虚拟机网卡重启失败
[Connection 'ens33' is not available on device ens33 because device is strictly unmanaged_victoruu的博客-CSDN博客](https://blog.csdn.net/vic_qxz/article/details/118863137)

报错
```go
Connection 'ens33' is not available on device ens33 because device is strictly unmanaged
```

解决, 查看托管状态
```bash

nmcli n
#显示 disabled 则为本文遇到的问题，如果是 enabled 则可以不用往下看了
#开启 托管
nmcli n on
```

但是依然失败
[解决 Error:No suitable device found: no device found for connection "System eth0"](https://blog.csdn.net/seven_zhao/article/details/43429571)
参考了上面的链接，
- 删除网卡
- 重新添加网卡
- 不重启也行，nmtui修改网卡名，手动改成以前的地址
- 重启网卡nmcli -c up ens37，即可恢复以前的所有链接！
现在ip有了，但是第二天发现无法连接外网，估计是<font color="#ff0000">dns或者是网关</font>不对，因为我手动配置了。后来这两个删了也是可以的。解决办法，删掉dns，网关，只保留了ip地址。改成自动获取。就好了。因为代码里的ip都是它。改成自动获取后我发现，dns竟然是它！
[[F.计算机学习笔记/Linux云计算/Linux基础/解决VMware centos8 网络问题\|解决VMware centos8 网络问题]]
![Pasted image 20230622103204.png](/img/user/Z.image/Linux/Pasted%20image%2020230622103204.png)