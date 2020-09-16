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

## CSS display 属性

| 值                 | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| none               | 此元素不会被显示。                                           |
| block              | 此元素将显示为块级元素，此元素前后会带有换行符。一个块级元素会新开始一行并且尽可能撑满容器。常用的块级包括: div，p，form，header，footer 等。 |
| inline             | 默认。此元素会被显示为内联元素，内联元素可以在段落中包裹一些文字而不会打乱段落的布局。元素前后没有换行符，无法设置width，height，不独占一行。常用的行内元素包括：span，a。 |
| inline-block       | 行内块元素，可设width，height。（CSS2.1 新增的值）           |
| list-item          | 此元素会作为列表显示。                                       |
| run-in             | 此元素会根据上下文作为块级元素或内联元素显示。               |
| table              | 此元素会作为块级表格来显示（类似 `<table>`），表格前后带有换行符。 |
| inline-table       | 此元素会作为内联表格来显示（类似 `<table>`），表格前后没有换行符。 |
| table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 `<tbody>`）。     |
| table-header-group | 此元素会作为一个或多个行的分组来显示（类似 `<thead>`）。     |
| table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 `<tfoot>`）。     |
| table-row          | 此元素会作为一个表格行显示（类似 `<tr>`）。                  |
| table-column-group | 此元素会作为一个或多个列的分组来显示（类似 `<colgroup>`）。  |
| table-column       | 此元素会作为一个单元格列显示（类似 `<col>`）                 |
| table-cell         | 此元素会作为一个表格单元格显示（类似 `<td>` 和 `<th>`）      |
| table-caption      | 此元素会作为一个表格标题显示（类似 `<caption>`）             |
| inherit            | 规定应该从父元素继承 display 属性的值。                      |