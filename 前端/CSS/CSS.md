[toc]

## 参考文档

[css隐藏页面元素的几种方法比较]:(http://www.divcss5.com/jiqiao/j50687.shtml)
[CSS3 transition介绍]:(https://www.jianshu.com/p/56f8ddafc63f)
[深入理解CSS过渡transition]:(https://www.cnblogs.com/xiaohuochai/p/5347930.html)
[CSS中的三种样式来源：创作人员、读者和用户代理(转载)]:(https://www.cnblogs.com/JJJJJKKKKK/articles/4542545.html)
[CSS中的样式覆盖原则]:(https://www.cnblogs.com/liuyonglong/p/3707816.html)

## 隐藏元素

### display:none

设置display:none的元素不会再占用页面控件，其占用的空间会被其他元素占有，从而引起浏览器的重排和重绘。设置该属性元素绑定的事件不会生效。设置该属性的元素会直接从页面消失，因此定义transition效果完全无效。

### visibility:hiddle

设置visibility:hiddle能够隐藏元素，但是该元素仍会占用页面控件，因此只会导致浏览器的重绘而不会重排。设置该属性元素绑定的事件不会生效。设置该属性的元素会在transition设置的时间内消失，但没有动画效果。

### opacity:0

设置元素透明度opacity:0也可以隐藏页面元素，但是元素依然会占据页面空间。设置该属性元素绑定的事件依然会生效。设置改属性的元素以动画效果消失。

## CSS过渡transition

//TODO

## CSS 样式来源

//TODO

## CSS 样式覆盖规则

//TODO

## CSS 选择器

//TODO