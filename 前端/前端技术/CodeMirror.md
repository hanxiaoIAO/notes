## CodeMirror

CodeMirror 是一款在 JavaScript 中为浏览器实现的多功能文本编辑器。它专门用于编辑代码，并附带许多语言模式和附加组件，实现更高级的编辑功能。

丰富的编程 API 和 CSS 组织管理系统可用于自定义 CodeMirror 以适应您的应用程序，并扩展其新功能。

CodeMirror主要用于扩展textarea标签。

```
1.引入js和css库
<link rel="stylesheet" href="codemirror-5.12/lib/codemirror.css">
<script src="codemirror-5.12/lib/codemirror.js"></script>
<script src="codemirror-5.12/clike.js"></script>

<!--引入css文件，用以支持主题-->
<link rel="stylesheet" href="codemirror-5.12/theme/seti.css">

2.js脚本
<script type="text/javascript">
    var editor=CodeMirror.fromTextArea(document.getElementById("code"),{
        mode:"text/x-java",
        lineNumbers:true,
        theme:"seti"
    });
</script>
```

