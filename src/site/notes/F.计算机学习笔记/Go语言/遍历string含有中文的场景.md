---
{"dg-publish":true,"dg-permalink":"遍历string含有中文的场景","permalink":"/遍历string含有中文的场景/","noteIcon":"","created":"2023-03-29","updated":""}
---

## 代码示例
---
```go
import (
  "fmt" 
  "testing"
)

func Test(t *testing.T){
  var s string 
  s="bowen"
  fmt.Println(len(s))
  for i, v := range s {
		fmt.Printf("%d %v\n", i, string(v)) // %v的话不会输出字符串本身，输出的是字符串的对应的ASCII值,所以后面要有string(v)
	}

s1:="少玩手机多编程序"
for i,v:=range s1{
  fmt.Printf("%d %v\n",i,string(v))
 }
}
```

运行截图
![Pasted image 20230627174105.png](/img/user/Z.image/Go/Pasted%20image%2020230627174105.png)

## 分析
---
1. 注意，<span style="background:rgba(3, 135, 102, 0.2)">testing包是小写的</span>，我一开始在[replit](https://replit.com/@sunnydongbowen/GoPractice)  运行的时候总是报错。以为这里不能用。
2. 注意 import的时候是没有逗号分隔的，我一开始写了逗号。
3. 注意 索引，可以看到字符串的索引是占了3。而不是1个。
4. 注意要用<span style="background:#d3f8b6">string(v)</span> 处理一下。不然输出的是ASCII码值。

## 补充go test
---
注意这是_test.go结尾的文件，<span style="background:rgba(5, 117, 197, 0.2)">不能go run运行，需要使用go test 运行</span>。<span style="background:#d3f8b6">且需要加-v</span>参数，不然不会打印出来东西的。
```bash
go test -v string_test.go
```
