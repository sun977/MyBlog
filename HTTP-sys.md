### HTTP.sys远程代码执行

#### 漏洞介绍：

HTTP.sys是Microsoft Windows处理HTTP请求的内核驱动程序，为了优化IIS服务器性能，从IIS6.0引入，IIS服务进程依赖HTTP.sys。**HTTP.sys远程代码执行漏洞实质是HTTP.sys的整数溢出漏洞**，当攻击者向受影响的Windows系统发送特殊设计的HTTP 请求，HTTP.sys 未正确分析时就会导致此漏洞，成功利用此漏洞的攻击者可以在系统帐户的上下文中执行任意代码。

影响环境：Windows+IIS的环境下，任何安装了微软IIS 6.0以上的Windows Server 2008 R2/Server 2012/Server 2012 R2以及Windows 7/8/8.1操作系统都受到这个漏洞的影响。



#### 漏洞知识：

说到HTTP.sys远程代码执行漏洞，不得不先介绍一下Range首部字段。

在“上古时代”，网络并不是很好，下载大型文件很不容易。下载途中如果网络中断，就得重头开始下。为了解决这个问题，HTTP/1.1引入了范围请求。

在请求报文的Range首部字段中指定资源的byte范围，告诉服务器，请求的是资源哪个范围的内容，让断点续传和并行下载得以实现。

如果服务器支持范围请求，响应包中就会存在Accept-Ranges字段(且值不为“none”，bytes为资源范围的单位)，并在Content-Length字段中告诉客户端资源的大小范围。

![img](https:////upload-images.jianshu.io/upload_images/8628147-e23d162263991d6c?imageMogr2/auto-orient/strip|imageView2/2/w/921/format/webp)

如果没有Accept-Ranges字段，则服务器可能不支持范围请求，有的服务器会明确将值设为“none”。

服务器面对范围请求，有三种响应：

请求成功：

响应206Partial Content请求范围越界：（范围超过资源的大小）

响应416Requested Range Not Satisfiable不支持范围请求：

响应200OK

而HTTP.sys远程代码执行漏洞正是利用Range字段注入恶意数据。该漏洞的检测，也是利用服务器面对范围请求时的响应特征来判断。





#### 漏洞检测方法：

1、先判断目标环境是否为Windows+IIS

2、然后构建Range字段进行检测即可

**检测时**，在请求包中添加Range字段，如下：

 **Range: bytes=0-18446744073709551615**

【18446744073709551615的十六进制为0xFFFFFFFFFFFFFFFF(16个F)是64位无符号整数所能表达的最大整数，整数溢出和这个超大整数有关】

然后go给服务器

```
GET / HTTP/1.1
Host: stuff
Range: bytes=0-18446744073709551615
```

或者：

```
# curl -v www.test.com -H "Host: irrelevant" -H "Range: bytes=0-18446744073709551615"
```

服务器响应 400，证明不存在HTTP.sys远程代码执行漏洞

```
HTTP Error 400. The request has an invalid header name.
```

服务器响应 416，则证明存在该漏洞

```
HTTP/1.1 416 Requested Range Not Satisfiable
Content-Type: text/html
Last-Modified: Thu, 22 Aug 2013 23:53:12 GMT
Accept-Ranges: bytes
ETag: "2edebc2929fce1:0"
```



#### 漏洞利用方法：



#### 漏洞修复建议：

升级安全补丁