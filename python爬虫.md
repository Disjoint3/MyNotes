# P9 13:36

# 爬虫技术

## 介绍及概念

- 网络爬虫(又被称为网页蜘蛛，网络机器人)就是模拟浏览器发送网络请求，接收请求响应，一种按照一定的规则，自动地抓取互联网信息的程序。
- 原则上，只要是浏览器(客户端)能做的事情，爬虫都能够做
- 通用爬虫软件：八爪鱼、火车采集器
- 其实只要能够发送HTTP (s)请求的任何编程语言都是可以做爬虫的，像C语言、C++、java、php、js等
- 根据被爬网站的数量不同，把爬虫分为：通用爬虫和聚焦爬虫

## 爬虫的流程

![image-20231125155747149](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125155747149.png)

**最难的是url是什么。**

1. 向起始url发送请求，并获取响应
2. 对响应进行提取
3. 如果提取url，则继续发送请求获取响应4.如果提取数据，则将数据进行保存

## 案例分析

一般而言，数据都在html、js和json

### 斗鱼图片

#### 分析

正常情况下，用浏览器的“检查”，可以定位到要下载的照片，一般是“img”标签中的“src”属性，也就知道了这个图片的URL。例如：

![image-20231125160517854](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125160517854.png)

#### 进一步分析

不正常情况下，有些网站为了反爬虫，放在了其他地方，因此需要自己分析。此时进行进一步分析。

流程

1. 右击>检查

2. 定位到要下载的妹子照片

3. 发现它不是一个img，而是一个div

4. 找到浏览器的network，刷新浏览器请求，找到这个图片，也就知道了请求的URL

5. 找到URL之后，要思考一个问题: 这个URL到底在哪里?

6. 点击”三个点”->"search"

   <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125161811696.png" alt="image-20231125161811696" style="zoom:50%;" />

7. 将URL粘贴，然后回车 查找

8. 找到了URL所在的文件
   ![image-20231125161841396](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125161841396.png)

9. 也就确定了此URL所在的位置 https://wwwdouyun,com/g_yz的response中



### 抖音视频

#### 链接准备

1. 获取需要的抖音视频的链接

   <img src="https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125162713458.png" alt="image-20231125162713458" style="zoom:50%;" />

2. 需要下载的抖音视频地址：
   儿子捡破烂存了1W多，你们觉得捡破烂丢人吗? 我教育他靠自己的双手挣的最干净都是光荣的，不丢人。大家觉得我说吗? https://v.douyin.com/Jacf7Uc/ 复制此链接，打开抖了 直接观看视频!

#### 分析

1. 打开新网页，设置好“设备仿真”。
2. 通过“XHR”查看浏览器请求情况，在请求中找视频地址。
3. 如果请求报文是“302”，表示要跳转访问。此时查看回复报文找到新跳转的地址。（请求和回复报文在一条记录里）
4. 对比下一条记录，会发现此时请求的地址就是需要跳转的新地址。如果是“200”，表示就是访问的这个网址。
5. 接着在这一条记录中去分析。 

水印的英文名为“watermark”，抖音的视频地址中“playervm”，去掉“vm”，即可找到无水印的视频。

![image-20231125170803336](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125170803336.png)

### 百度地图商家

#### 分析

查看方法和前面基本一致，使用了“模拟设备”。

##### 商家

打开“预览”后，查看可以找到商家对应的链接：

![image-20231125172454033](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125172454033.png)

##### 页数

查找药店后，发现是一页一页显示的，一页10个商家。“XHR”显示如下：

![image-20231125172210752](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125172210752.png)

按了“下一页后”，“XHR”显示如下：

![image-20231125172230653](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125172230653.png)

接着就可以对比不同页的链接的不同，从而找到不同页数的规律。

对比不同可以找相关的在线网址。



#### 拓：URL编码

![image-20231125172703706](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonCrawlerimage-20231125172703706.png)

请求报文中的链接出现了一些百分号什么什么的，这些是URL编码后的。想要知道真正的内容，需要继续宁解码。

搜索引擎可以搜到在线编码解码的网站。

### 淘宝评论

复制URL的链接后，可能不会出现想要的数据，这是因为网站通过一些方式进行了反爬。

## HTTP和HTTPS复习

- 在发送请求，获取响应的过程中 就是发送HTTP或HTTPS的请求，获股HTTS的响应。
- HTTP端口：90
- HTTPS端口：443

### 拓：与TCP

HTTP/HTTPS就是在TCP的基础上，发送的一个很长很长的字符串。用特定的格式来对字符串进行处理发送接收然后再处理，这个约定的格式就是协议。

例如：

利用“网络调试助手”担当服务端，随意找个浏览器输入“ip:port”的形式，可以连接到服务端。此时在服务端中回复以下内容：

```http
HTTP 200 OK

hello world
```

发送后浏览器不会显示错误，但是也不会显示发送的内容。当与服务端的连接断开时，网页会显示“hello world”。



