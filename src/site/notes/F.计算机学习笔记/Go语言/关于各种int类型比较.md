---
{"dg-publish":true,"dg-permalink":"关于各种int类型比较","permalink":"/关于各种int类型比较/","noteIcon":"","created":"2023-03-19","updated":""}
---


## 代码示例
---

```go
import (
  "fmt"
  "testing"
  "math"
  "unsafe"
)

func TestInt(t *testing.T){
  var i1 int =1
  var i2 int8=2
  var i3 int16=3
  var i4 int32=4
  var i5 int64=5
  var i6 uint64=6

  fmt.Printf("int    : %v\n",unsafe.Sizeof(i1))
  fmt.Printf("int8    : %v\n",unsafe.Sizeof(i2))
  fmt.Printf("int16    : %v\n",unsafe.Sizeof(i3))
  fmt.Printf("int32    : %v\n",unsafe.Sizeof(i4))
  fmt.Printf("int64   : %v\n",unsafe.Sizeof(i5))
  fmt.Printf("uint64    : %v\n",unsafe.Sizeof(i6))  
}


func TestRange(t *testing.T){
  fmt.Println("int ",math.MinInt,"~",math.MaxInt)
  fmt.Println("int8 ",math.MinInt8,"~",math.MaxInt8)
  fmt.Println("int16 ",math.MinInt16,"~",math.MaxInt16)
  fmt.Println("int32 ",math.MinInt32,"~",math.MaxInt32)
  fmt.Println("int64 ",math.MinInt64,"~",math.MaxInt64)
}
```

![Pasted image 20230627194908.png](/img/user/Z.image/Go/Pasted%20image%2020230627194908.png)


## 注意点
---
<span style="background:rgba(5, 117, 197, 0.2)">这里看到，还是在Linux命令行运行脚本比较有感觉。</span>  和在windows上运行两种不同的概念。
int 类型大小为 8 字节，8byte  1byte=8bit，int和int64是一样的了。 
int8 类型大小为 <span style="background:rgba(3, 135, 102, 0.2)">1 字节 1_8bit = 8bit</span> ，int8类型能表示的数并不是很大。
int16 类型大小为 <span style="background:rgba(3, 135, 102, 0.2)">2 字节 2_8bit = 16b</span>it ，int16类型能表示的数也不是很大。
int32 类型大小为<span style="background:rgba(3, 135, 102, 0.2)"> 4 字节 4_8 bit =32bit </span>
int64 类型大小为 <span style="background:rgba(3, 135, 102, 0.2)">8 字节 8_8 bit =64bit</span>
很好记忆，是8的倍数。几倍就是几个字节，然后就是多少位。可以看到int类型的可以表示的数已经很大了。

> **go语言中的int的大小是和操作系统位数相关的，如果是32位操作系统，int类型的大小就是4字节; 如果是64位操作系统，int类型的大小就是8个字节**，例如这是我在replit上运行的，是8个字节，1个字节是16位。可以画个图理解一下。说明这是64位的机器。

uint8: 0 ~ 255 
uint16: 0 ~ 65535 
uint32: 0 ~ 4294967295
uint64: 0 ~ 18446744073709551615
> 注意uint和int表示的范围是不一样的。在编程中如果明确知道了不会出现负数或者是限制数大小，就可以明确规定数据类型。

## 补充
---
math库里面有不少方法，可以点进去看下。不要说go不如py什么的。看看里面给我们提供了哪些计算方法。
[[F.计算机学习笔记/Linux云计算/Linux基础/视频笔记~python+Linux\|视频笔记~python+Linux]]

