---
{"dg-publish":true,"dg-permalink":"进程及cpu和内存占用","permalink":"/进程及cpu和内存占用/","noteIcon":"","created":"2021-01-09","updated":""}
---


# 1、知道进程名称，查看占用的cpu和内存
---
思路
- 查看进程的pid
- 根据进程的pid，查看 cat /proc/42635/status
- 或者 top -p pid【重要】
```bash
[root@ocloud-122 ~]# ps -aux|grep java
root      3924  0.0  0.0 221860  1052 pts/54   S+   14:06   0:00 grep --color=auto java
root     42635  0.2  1.0 55031288 3515196 ?    Sl   May13   2:36 java -jar vmanager-0.0.1-SNAPSHOT.jar
root     42806  0.1  0.3 39989268 1225668 ?    Sl   May13   1:50 java -jar ocloud-login-0.0.1-SNAPSHOT.jar
```

```bash
cat /proc/42635/status
```

```bash
top -p 42635
```

[/proc/pid/status解释](http://blog.chinaunix.net/uid-24347760-id-2943156.html)

# 2、根据pid号，查看占用程序的所在目录
---
- 找到pid
```bash
top -c
11659 mssql     20   0   16.1g   2.6g   3600 S  98.0  8.4  16511:22 /opt/mssql/bin/sqlservr
 1498 root      20   0   11.6g   3.0g   4564 S   6.0  9.5   1891:35 /usr/bin/java -Dspring.profiles.active=dev -Dspring.config.location=./application.+
29368 mysql     20   0 2661296 472816   2412 S   4.3  1.4   1304:30 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/ocloud/mysqldata+
25538 root      20   0   12.7g 999.2m  14588 S   2.0  3.1  10:09.07 java -jar -Dspring.profiles.active=prod tbmmonitor_master_V1.6.4022_back.jar
 2693 root      20   0  114076   2384   1328 S   0.7  0.0   0:14.25 bash -c while [ -d /proc/$PPID ]; do sleep 1;head -v -n 8 /proc/meminfo; head -v -+
```

- 查看目录
---
```bash
[root@ocloud ~]# cd  /proc/7719/
[root@ocloud 7719]# ll
total 0
dr-xr-xr-x  2 root root 0 Jan  7 16:26 attr
-rw-r--r--  1 root root 0 Jan  7 16:26 autogroup
-r--------  1 root root 0 Jan  7 16:26 auxv
-r--r--r--  1 root root 0 Jan  7 14:04 cgroup
--w-------  1 root root 0 Jan  7 16:26 clear_refs
-r--r--r--  1 root root 0 Jan  7 14:05 cmdline
-rw-r--r--  1 root root 0 Jan  7 16:26 comm
-rw-r--r--  1 root root 0 Jan  7 16:26 coredump_filter
-r--r--r--  1 root root 0 Jan  7 16:26 cpuset
lrwxrwxrwx  1 root root 0 Jan  7 16:26 cwd -> /ocloud/tbmmonitor/tbmmonitor-interface
-r--------  1 root root 0 Jan  7 16:26 environ
lrwxrwxrwx  1 root root 0 Jan  7 14:04 exe -> /usr/java/jdk1.8.0_251-amd64/jre/bin/java
dr-x------  2 root root 0 Jan  7 15:29 fd
dr-x------  2 root root 0 Jan  7 16:26 fdinfo
```

进入目录，就能看到文件目录了。可以看到，是/ocloud/tbmmonitor/tbmmonitor-interface目录下的，定位到是这个目录下jar包占用内存异常。

# 3、ps查看
---

- e 是所有进程都显示出来
- f 做一个更完整的输出

```bash
#  这样直接定位到这个jar包本身，也是一种方法。
[root@ocloud 7719]# ps -aux |grep -v grep|grep 7719
root      7719  6.7  5.0 12117452 1643088 pts/0 Sl  14:04  10:10 /usr/bin/java -Dspring.profiles.active=dev -Dspring.config.location=./application.yml -jar tbm-data-collect-0.0.1-SNAPSHOT.jar
```

[参考链接](https://www.cnblogs.com/jie-fang/p/7686521.html)

# 4、查看top10(内存和cpu)
---
```bash
 ps -aux | sort -k4nr | head -10
```

sort -k4nr中（k代表从根据哪一个关键词排序，后面的数字4表示按照第四列排序；n指代numberic sort，根据其数值排序；r指代reverse，这里是指反向比较结果，输出时默认从小到大，反向后从大到小。）。本例中，可以看到%MEM在第4个位置，根据%MEM的数值进行由大到小的排序。-k3表示按照cpu占用率排序。

查看占用cpu较高的top10的程序。

```bash
ps -aux | sort -k3nr | head -10
```