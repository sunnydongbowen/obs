---
{"dg-publish":true,"dg-permalink":"解决ssh失败问题","permalink":"/解决ssh失败问题/","noteIcon":"","created":"2021-01-09","updated":""}
---

 ## 报错一
--- 
这个报错通常在主机重装了系统，但是ip没变的场景。

```bash
[root@os53 ~]# scp chrony.tar 192.168.10.112:/root/openstack
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:HZ+A154W6mg8MQkJhuxIZW2GV/Vb4ZwfdJleFAqdl2A.
Please contact your system administrator.
Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /root/.ssh/known_hosts:16
ECDSA host key for 192.168.10.112 has changed and you have requested strict checking.
Host key verification failed.
lost connection
```


解决,去下面这个文件，然后dd掉scp的ip这行。
```bash
/root/.ssh/known_hosts
```

## 报错2

ssh文件配置问题，改成yes
```bash
PasswordAuthentication yes
```

## 报错3
---
前不久遇到一次，可以ssh，但是进不去这个用户的bash，也无法上传文件。操作一通，大概率是因为磁盘配额满了。