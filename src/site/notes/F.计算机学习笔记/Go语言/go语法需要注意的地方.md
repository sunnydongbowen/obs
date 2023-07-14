---
{"dg-publish":true,"dg-permalink":"go语法需要注意的地方","permalink":"/go语法需要注意的地方/","noteIcon":"","created":"2023-07-03","updated":""}
---

## 变量声明
---
go的声明是永远都是变量名在前面，类型在后面。我在使用replit敲时就犯了这个错误，导致一直给我报错，原因是我写错顺序了！
![Pasted image 20230627202811.png](/img/user/Z.image/Go/Pasted%20image%2020230627202811.png)

![Pasted image 20230627202839.png](/img/user/Z.image/Go/Pasted%20image%2020230627202839.png)
> 平时都用goland编写，有些错误确实不注意就这样了。你看上面就报编译错误了吧。

## 导入包必须要用，否则编译不过去
---
比如我导入了一个包，但是我没使用。编译的时候就会报错。
![Pasted image 20230627203008.png](/img/user/Z.image/Go/Pasted%20image%2020230627203008.png)

看到没，这一点用goland是没发现的，因为goland会自动帮我们去掉不用的包。这一点我想提前导入都不行，因为它会自动去掉。

## 声明的变量必须要用
---
声明了返回值或者是变量必须要用，不用的话编译也会报错。
![Pasted image 20230627203237.png](/img/user/Z.image/Go/Pasted%20image%2020230627203237.png)
这也是使用replit发现的。平时使用goland根本不注意。

## 函数返回值必须一致
---
看下面报错

![Pasted image 20230627203349.png](/img/user/Z.image/Go/Pasted%20image%2020230627203349.png)

这是因为我一个返回值命名了，另外一个没有。类似下面这样
```go
func sum1(a,b int) (sum int,error){
```
于是就报错了，也就是说，如果不命名就都不命名，要命名就都命名。
看到了没，这些问题要不是在replit敲还真发现不了。还是Linux适合编程一些啊！

## 包名
---
1. 我在import包的时候注意包名<span style="background:rgba(3, 135, 102, 0.2)">一般是小写</span>，而包名的方法一般是大写。这一点要注意。没有goland就需要自己去import包名。
2. 注意package 声明。不要和import弄混。
3. <font color="#c00000">注意包名用英文，不要用中文</font>！

## go run .
---
当很多文件，只有一个main入口函数。我们需要进入这个包下面<span style="background:rgba(3, 135, 102, 0.2)">go run . </span>，而不是go run xxx.go , 这样是找不到其他文件定义的变量和函数的。

![Pasted image 20230628104640.png](/img/user/Z.image/Go/Pasted%20image%2020230628104640.png)

这在命令行很容易看出来，不<font color="#c00000">要过度依赖goland，发现不了问</font>题。goland需要在这个目录下点run，而不是直接右击代码.run，不然也是一样的报错。

> 而且go run也是有-v 参数的。 go run -v xxx.go

## main 函数不能在一个包里重复出现
---
同一个包里只能有一个main函数。例如我有两个代码都写了main函数。那么
就会报错了。

![Pasted image 20230628162557.png](/img/user/Z.image/Go/Pasted%20image%2020230628162557.png)

## go run的必须是带pakage main的
---

![Pasted image 20230629144109.png](/img/user/Z.image/Go/Pasted%20image%2020230629144109.png)


>用go run 跑函数，必须带package main，而不是其他包的声明。不然是会报上面错误.

## main函数尽量放外面
---

![Pasted image 20230703110045.png](/img/user/Z.image/Go/Pasted%20image%2020230703110045.png)


这个是我在运行单元测试遇到的，为什么会有这个错误，是因为我把这个文件夹下的包声明成了package main，因为这个程序是带main函数的，尽管它只是一个测试程序。所以我这样写是不规范的。<font color="#c00000">正常的只能有一个main函数。且其他包的package声明尽量一致</font>。所以我之前的做法是不规范的。这就是在Linux命令行下运行和在windows下运行的区别。

看看下面的报错！所以不要随随便便的去写main函数，声明main包。平时的demo用test方式去练习就好了。正儿八经的项目只有个main包和main入口的！

![Pasted image 20230703102935.png](/img/user/Z.image/Go/Pasted%20image%2020230703102935.png)

## gofmt
---
在使用goland过程中，自动化格式化代码了，但是我在replit中，想格式化代码，没找到按钮。使用gofmt格式化 但是这样只能格式Linux下的展示。web ide里都没有格式化出来。后面再找找吧，肯定有格式化的地方。

![Pasted image 20230628162926.png](/img/user/Z.image/Go/Pasted%20image%2020230628162926.png)


## go test
---
之前一直是使用goland进行go test，很好用。需要跑哪一个，在代码里右击单独跑就可以了，需要跑哪一本，直接运行就都跑了。但是命令行中我们需要注意一种情况，如果说这个测试文件引用了其他文件的变量，就不能单独go test -v xxx.go去跑了，会找不到这个文件。例如

![Pasted image 20230628165501.png](/img/user/Z.image/Go/Pasted%20image%2020230628165501.png)

下面这个跑法是正确的。

![Pasted image 20230628165432.png](/img/user/Z.image/Go/Pasted%20image%2020230628165432.png)
剩余有些命令可以[参考这里](http://c.biancheng.net/view/124.html)

<span style="background:rgba(3, 135, 102, 0.2)">假如我要运行某个单元测试，就需要,  关键还是. 和-run 测试函数名</span>  这个命令很重要，可以单独帮我们测试需要的函数。
```bash
go test -v -run TestContext  .
```

> go test 后面会详细介绍，要注意，即便是我们跑的是单元测试，如果这个包中其他代码有编译性的错误，也是会报错的！<font color="#c00000">跑单独的某个函数时一定要加run，单个测试文件不需要加run！</font>


