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
  2. POST：用于表单提交。
  3. HEAD/OPTIONS/PUT：
  4. CONNECT/TRACE/TRACK：出于安全风险的考虑，被禁止使用。

- 参数2：URL。

- 参数3：石头异步发送，布尔值，默认为 true，异步发送。

- 参数4、5：如果 URL 受密码保护，可提供第四（用户）第五（密码）个参数。

### 接收响应

一个完整的 HTTP 响应由状态码、响应头集合和响应主体组成。收到响应后，可以通过 XHR 对象的属性和方法使用。

响应中常用的四个属性：

>状态码 - status：HTTP 状态码（数字形式）
>
>状态码 - statusText：HTTP 状态说明（文本形式）
>
>响应主体 - responseText：作为响应主体被返回的文本（文本形式）。无论内容类型是什么，响应主体的内容都会保存到responseText属性中
>
>响应主体 - responseXML：作为响应主体被返回的文本（XML 形式）。响应的内容类型是'text/xml'或'application/xml'

### XHR对象的readyState属性

异步响应可以使用 XHR 对象的 readyState 属性，该属性表示请求/响应过程中的当前活动阶段。这个属性可取值：

> 0(UNSENT):未初始化。尚未调用open 方法
>
> 1(OPENED):启动。已经调用open()方法，但尚未调用send()方法
>
> 2(HEADERS_RECEIVED):发送。己经调用send()方法，且接收到头信息
>
> 3(LOADING):接收。已经接收到部分响应主体信息
>
> 4(DONE):完成。已经接收到全部响应数据，而且已经可以在客户端使用了

理论来说，只要 readyState 属性变化，都会触发一次 readystatechange 事件。

注： 必须在调用open()之前指定onreadystatechange 事件处理程序才能确保跨浏览器兼容性，否则将无法接收readyState属性为0和1的情况。

### 超时 timeout 与 ontimeout()

整数，标识多少毫秒之后，如果请求仍然没有得到结果，就会自动终止。默认等于 0 ，表示没有事件限制。

如果请求超时，将触发 ontimeout 事件

## 参考

[什么是xhr?](https://blog.csdn.net/m_s_l/article/details/89460964)

[深入理解ajax系列第一篇——XHR对象](https://blog.csdn.net/weixin_33827965/article/details/85830502?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control)