## 服务器和客户端（浏览器）的交互过程

输入网址后，浏览器先访问本地Host文件，查看Host文件中是否包含请求的域名，有则返回对应的ip,没有则访问公网DNS系统，查找对应的的ip。找到ip之后，浏览器向该ip的服务器发出请求。服务器接收到请求后进行处理，然后返回静态的文件。服务器接收到之后展示出来。

js 与服务器的交互的整体流程类似，区别在于js与服务器的交互不会主动刷新页面，可以只返回想要的数据。

## URL-统一资源定位器 (Uniform Resource Locators)

Web 浏览器通过 URL 从 Web 服务器请求页面。

语法规则：

```
scheme://host.domain:port/path/filename
```

说明：

> - Scheme：定义因特网服务的类型。常见类型是 http
> - host：定义域主机，http 的默认主机是 www
> - domain：定义因特网域名
> - port：定义主机上的端口号
> - path：定义服务器上的路径，如果省略，则文档必须位于网站的根目录中
> - filename：定义文档/资源的名称

### 常见的 URL Scheme

| Scheme | 访问               | 用于...                             |
| ------ | ------------------ | ----------------------------------- |
| http   | 超文本传输协议     | 以 http:// 开头的普通网页。不加密。 |
| https  | 安全超文本传输协议 | 安全网页，加密所有信息交换。        |
| ftp    | 文件传输协议       | 用于将文件下载或上传至网站。        |
| file   |                    | 您计算机上的文件。                  |

## HTML5 文件上传探讨

需求主要包括这么几个方面:

- 基本需求：
  1. 可拖拽
  2. 具有上传进度显示
  3. 支持多文件同时上传
- 浏览器支持：
  1. IE8 到最新版
  2. Firefox 和 Chrome
  3. 能够处理上传完成后服务器返回的 JSON 格式信息

候选者：

- Stream: http://www.oschina.net/p/stream
  - Uploadify的Flash版和Html5版的结合, 对旧的浏览器的兼容性应该比较好
- Resumable.js: http://www.oschina.net/p/resumable-js
  - 多路同步、稳定和可恢复的文件上传，基于 HTML5 File API; 貌似比较高端，不知道兼容性如何；
- Plupload: http://www.plupload.com/
  - 具备 GPL 和 商业授权 双授权协议的版本，功能应该比较不错；
- YUI Uploader 的例子: http://yuilibrary.com/yui/docs/uploader/uploader-dd.html
  - 现成的例子，可以试试
- Html5 File Upload with Progress: http://www.matlus.com/html5-file-upload-with-progress/
  - 一篇技术文章，对了解原理比较有好处；