## 介绍

Vue 是渐进式框架，自底而上逐层应用，核心库只关心视图层。

Vue 是响应式的，HTML 是一个入口，数据与 DOM 建立关联，DOM 元素由 Vue 实例完全控制。（// 基于 Runtime框架）

## 语法 - HTML 部分

文本绑定："Mustache" 语法（双大括号）

```js
<span>Message: {{ msg }}</span>
```

一次性文本插值：v-once 指令

```js
<span v-once>这个将不会改变: {{ msg }}</span>
```

原始 HTML：v-html 指令

```js
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

绑定 attribute：v-bind 指令，`isButtonDisabled` 可以为字符串、`true` 、`null`、`undefined` 或 `false`

```js
<button v-bind:disabled="isButtonDisabled">Button</button>
<!-- 缩写 -->
<button :disabled="isButtonDisabled">Button</button>
```

绑定attribute->class/style：v-bind 指令。针对 class ，表达式结果做了增强，类型除了字符串之外，还可以是对象或数组。style与class类似。

```js
<div v-bind:class="classObject"></div>
<!-- class 存在与否将取决于数据 property isActive 的 truthiness-->
<div v-bind:class="{ active: isActive }"></div>
<!-- 可以与普通的 class attribute 共存 -->
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
<div v-bind:class="[activeClass, errorClass]"></div>
```

绑定动态参数：方括号括起来 JavaScript 作为指令参数。但空格和引号，放在 HTML attribute 名里是无效的。

```js
<a v-bind:[attributeName]="url"> ... </a>
<!-- 缩写(2.6.0+) -->
<a :[attributeName]="url"> ... </a>
```

JavaScript 表达式：

```js
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('') }}
<div v-bind:id="'list-'+id'"></div>
```

## 语法 - JS 部分

```
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```

### 数据

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

### 方法

```js
<p>Reversed message: "{{ reversedMessage() }}"</p>
// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```

### 钩子

created 钩子可以用来在一个实例被创建之后执行代码。除此之外还有在实例其他不同生命周期调用的钩子，如 mounted、updated 和 destroyed。

```js
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1
```

### 计算属性

计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性默认为 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```

```js
// 计算属性的 setter
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: {
      // getter
      get: function{
      	return this.message.split('').reverse().join('')
      }
      //setter
      set: function(newReversedMessage){
      	this.message = newReversedMessage.split('').reverse().join('')
      }
    }
  }
})
```

### 侦听

侦听适用于异步或开销较大的操作

```
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
    reversedMessage：'olleH';
  },
  watch: {
  	message: function(newmessage,oldmessage){
  		this.reversedMessage = newmessage.split('').reverse().join('')
  	}
  }
})
```

