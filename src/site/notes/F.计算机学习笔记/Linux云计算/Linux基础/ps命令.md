---
{"dg-publish":true,"dg-permalink":"ps命令","permalink":"/ps命令/","noteIcon":"","created":"2022-09-19","updated":""}
---


## ps命令
---
- 我一般不用这个
```bash
ps aux 
```

- 用下面这个多一些
```bash
ps -ef | grep
```

- 查看某个id是被哪个进程占用的
```bash
ps -p  id
```

```bash
cat num.pid |xargs ps -p
```

xargs 是 execute arguments 的缩写，它的作用是从标准输入中读取内容，并将此内容传递给它要协助的命令，并作为那个命令的参数来执行。

注意和lsof区分，lsof -i: 查的是端口号