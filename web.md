# HTML5 文件上传探讨

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