# 爬虫

## requests & Beautifulsoup

### 常见提取元素的方法

- Beautifulsoup：soup.select(" ") 配合使用 infolite插件
- xpath：配合插件xpath使用
- 正则表达式

### request的使用

- ​	

### bs的使用

- scrapy 使用bs4：
- selenium使用bs: Beautifulsoup(driver.page_source)

## Scrapy

### Scrapy文件目录

- 创建项目  `scrapy startproject weibo`

文件目录

```
weibo
    weibo
        spiders
            __init__.py
        __init__.py
        items.py  
        middlewares.py
        pipelines.py
        setting.py
    main.py
    scrapy.cfg scrapy的配置文件
```

## 采集javascript

采集js的几种方法

- 模拟浏览器：phantomjs，pyv8等等工具，效率低，不适合大规模的爬取
- 更换爬取的网址，移动端或者app或者google 缓存等等、
- 解析js源码：较为困难

### 常见js命令

- 将页面拉至最底部：driver.execute_script('window.scrollTo(0,document.body.scrollHeight);')
- 当前浏览器窗口新的页面: window.open('http://index.baidu.com','_self')

### 解析js源码

- request_url中有一个token的参数或者其他的参数
- 找到参数，使用ctrl+shift+F进行全局搜索这个参数，找到相应的js文件
- 文件进行断点调试？？找到生成该参数的具体js代码??实际中如何更好的设置断点
- 解析js代码，并将js代码转化为python
- [携程机票js实例](http://wenqiang-china.github.io/2016/05/11/get-ctrip-flights-info-2/)
- any XHR   breakpoint，watch
- 带上cookie，看看文件的参数，搜索cookie

## 验证码和图像识别

## 常用工具

### chrome

[chrome 开发者工具](http://wiki.jikexueyuan.com/project/chrome-devtools/debugging-javascript.html)

## 其他知识

### OSI与TCP/IP 协议

- TCP/IP 一般分为3-5层，下面以4层为例
  - 应用层：HTTP，DNS 域名系统，FTP，Telnet
  - 传输层：TCP(传输控制协议)，UDP
  - 网络层：IP（网际协议）
  - 数据链层：SLIP,CSLIP,PPP

### HTTP网络请求状态

| 编码   | 状态     |
| :--- | :----- |
| 2xx  | 请求状态成功 |
| 3xx  | 重定向    |
| 4xx  | 客户端错误  |
| 5xx  | 服务器错误  |