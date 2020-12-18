## 简介

xhr(XML Http Request)，用于与服务器交换数据，是 ajax 功能实现所依赖的对象。

xhr 对象提供了对 HTTP 协议的完全访问，包括做出 POST 和 HEAD 请求以及普通的 GET 请求的功能。

xhr 可以同步或异步地返回 web 服务器的相应，并且能以文本或者 DOM 文档的形式返回内容。

xhr 接口强制要求请求具备严格的 HTTP 语义，浏览器格式化请求并管理连接的完整生命周期。

## 使用

### 创建 XHR 对象

```javascript
var xhr;
if(window.XMLHttpRequest){
    xhr = new XMLHttpRequest();
}else{
    xhr = new ActiveXObject('Microsoft.XMLHTTP');//在IE5中，XHR对象是通过MSXML库中的一个ActiveX对象实现的
}
```

### 发送请求

```javascript
xhr.open("get","example.php", false);
```

- 参数1：

  用于指定发送请求的方式。不区分大小写。常用的值有：

  1. GET：用于常规请求。



## 参考

[什么是xhr?](https://blog.csdn.net/m_s_l/article/details/89460964)

[深入理解ajax系列第一篇——XHR对象](https://blog.csdn.net/weixin_33827965/article/details/85830502?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control)