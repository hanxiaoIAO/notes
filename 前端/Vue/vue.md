## 介绍

Vue 是渐进式框架，自底而上逐层应用，核心库只关心视图层。

Vue 是响应式的，HTML 是一个入口，数据与 DOM 建立关联，DOM 元素由 Vue 实例完全控制。（// 基于 Runtime框架）

## 数据与方法

Vue 实例被创建时，将对象中的 property 加入到 Vue 系统中并建立关联关系，但是在 Vue 实例创建之后添加的属性不会存在关联关系。

除了数据属性，Vue 还提供了一些有用的实例属性和方法，都以 $ 为前缀。

```js
var body = { message: 1 }

// 该对象被加入到一个 Vue 实例中
var app = new Vue({
  el: '#example'
  data: body
})

body.message == app.message//=>true

body.text="hello";
app.text//undefine

app.$data === body//=>true
app.$el === document.getElementById('example')//=>true
app.$watch('message',function(newValue,oldValue){
    // 这个回调将在 'app.message' 改变后调用
})
```

