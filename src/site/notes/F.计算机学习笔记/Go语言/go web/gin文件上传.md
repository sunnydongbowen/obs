---
{"dg-publish":true,"dg-permalink":"gin文件上传","permalink":"/gin文件上传/","noteIcon":"","created":"2022-03-11","updated":""}
---

---

> 🙃上传文件是很常用的功能，oa，办公，财务，云平台，都会涉及上传表格，图片，镜像等信息。

# 单文件上传
---
```go
func TestUpload(t *testing.T) {
	r := gin.Default()
	//加载模板
	r.LoadHTMLFiles("upload.html")
	//请求上传文件页面
	r.GET("/upload", func(c *gin.Context) {
		c.HTML(http.StatusOK, "upload.html", nil)
	})

	r.POST("/upload", func(c *gin.Context) {
		file, err := c.FormFile("fl")
		if err != nil {
			c.JSON(http.StatusInternalServerError, gin.H{
				"message": err.Error(),
			})
			return
		}
		log.Println(file.Filename)
		//这里存到了本地，在实际项目中，更多的是存到了对象存储，例如mino，阿里云之类的;
		dst := fmt.Sprintf("D:/BaiduNetdiskDownload/%s", file.Filename)
		// 上传文件到指定目录
		c.SaveUploadedFile(file, dst)
		c.JSON(http.StatusOK, gin.H{
			"message": fmt.Sprintf("'%s' uploaded!", file.Filename),
		})
	})
	r.Run()
}
```

这个demo是我去年学习Go的时候，参考李文周的视频和博客写的，注意点
- html里面`<input type="file" name="fl">` , 是fl，不是f1，不要弄混了。
- 不要加`multiple`,这是单文件上传
- postman无法测试，这个要通过浏览器测试
这是我在replit上跑的结果。
![Pasted image 20230705102508.png](/img/user/Z.image/Go/Pasted%20image%2020230705102508.png)
运行程序后它会给出一个域名，然后我们访问域名和url。就可以上传文件，最后看到服务器文件上传成功。
![Pasted image 20230705102815.png](/img/user/Z.image/Go/Pasted%20image%2020230705102815.png)


本机运行结果:
![](/img/user/Z.image/Go/文件上传/20230401102220.png)




# 多文件上传
---
```go
func TestUploadMulti(t *testing.T) {
	r := gin.Default()

	// 加载模板
	r.LoadHTMLFiles("upload.html")
	// 上传文件
	r.GET("/upload", func(c *gin.Context) {
		c.HTML(http.StatusOK, "upload.html", nil)
	})

	r.POST("/upload", func(c *gin.Context) {
		// 多文件上传
		form, _ := c.MultipartForm()
		files := form.File["file"]  //此处有坑！

		for index, file := range files {
			log.Println(file.Filename)
			dst := fmt.Sprintf("D:/BaiduNetdiskDownload/%s_%d", file.Filename, index)
			// 上传文件到指定目录
			c.SaveUploadedFile(file, dst)
		}
		c.JSON(http.StatusOK, gin.H{
			"message": fmt.Sprintf("%d files uploaded!", len(files)),
		})
	})
	r.Run()
}

```

多文件上传，注意
- html里`<input type="file" name="fl  multiple`" 要有多选这个选项
- 可以用postman测试, 注意key写file
- 注意name这里要和html的name一致！！！

![](/img/user/Z.image/Go/文件上传/20230401104116.png)

后来在复习的时候在replit又敲了一次这段代码，结果发现获取的files总是0！最后发现是filename写错了！

# 小结
---
- 文件上传是基本且重要的功能，要结合后面实践使用
- 需要学习一下源码，是如何设计的
- 想一下，我们平时用的上传文件的功能是什么样子的，比如mino对象存储。它也是go写的。