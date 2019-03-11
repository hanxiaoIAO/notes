## blur() 方法

### 定义和用法

当元素失去焦点时发生 blur 事件。

blur() 函数触发 blur 事件，或者如果设置了 *function* 参数，该函数也可规定当发生 blur 事件时执行的代码。

```js
  $("input").focus(function(){
    $("input").css("background-color","#FFFFCC");
  });
  $("input").blur(function(){
    $("input").css("background-color","#D6D6FF");
  });
  $("#btn1").click(function(){
    $("input").focus();
  });  
  $("#btn2").click(function(){
    $("input").blur();
  }); 
```

