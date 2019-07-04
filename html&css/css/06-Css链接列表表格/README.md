# 课程目标

- 掌握超链接伪类选择器的用法
- 掌握超链接鼠标经过效果的应用
- 掌握列表属性在实际工作中的应用
- 掌握表格属性在实际工作中的应用

# 链接的样式

## 链接的状态

- a:link - 普通的、未被访问的链接
- a:visited - 用户已访问的链接
- a:hover - 鼠标指针位于链接的上方（必须写a:link和a:visited之后）
- a:active - 链接被点击的时刻 （必须写在最后）

```css
a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */
```

 注意：实际工作中链接的样式如此写

```css
a { color:#FF0000; }
a:hover { color:#FF00FF;}
```

## 伪类选择器

链接的状态即是链接的伪类选择器。实际使用最多的就是鼠标经过伪类":hover"。

鼠标经过超链接改变链接样式：

```css
a { /* 设置初始样式 */
    color:#333;
    background-color:#aaa;
}
a:hover{ /* 设置鼠标经过改变 */
    color:#fff;
    background-color:#f00;
}
```

**注意： IE6只能识别超链接上的伪类**

也可以给其他元素使用伪类选择器（在IE6浏览器中不兼容）

```css
li { /* 设置初始样式 */
    color:#333;
    background-color:#aaa;
}
li:hover{ /* 设置鼠标经过改变 */
    color:#fff;
    background-color:#f00;
}
```

伪类选择器配合后代选择器使用

```css
li ul { /* 设置初始样式 */
    display:none;
}
li:hover ul { /* 设置鼠标经过改变 */
    display:block;
}
```

## 鼠标样式cursor

设置鼠标指针采用何种系统预定义的光标形状。

语法：

```css
选择器 { cursor :  default | pointer  | move  |  text }
```

属性值：（部分）

1. default  箭头
2. pointer  点击手型
3.  move  移动
4. text  文本

# 列表的样式

| 属性                | 属性值 | 描述             |
| ------------------- | ------ | ---------------- |
| list-style-type     |        | 列表类型         |
| list-style-image    |        | 列表项图像       |
| list-style-position |        | 列表标志位置     |
| list-style          |        | 列表样式综合设置 |

##列表类型

设置列表的标志类型。

语法：

```css
ul { list-style-type : disc | circle | square | decimal | lower-alpha; }
```

属性值：（部分）

disc 实心圆

circle 空心圆

square  实心方块

decimal 阿拉伯数字

lower-alpha 罗马数字

## 列表项图像

设置一个图像作为列表的标志。

语法：

```css
ul li { list-style-image : none | url(URL); }
```

属性值：

1. none
2. URL

## 列表标志位置

设置列表的标志出现在内部还是外部。

语法：

```css
ul { list-style-position : inside | outside; }
```

属性值：

1. inside
2. outside

## 列表样式综合设置

综合设置列表的三个属性。

语法：

```css
ul { list-style : list-style-type  list-style-image  list-style-position;}
```

案例：

```
ul { list-style : square url(example.gif) inside ;}
```

list-style 的值可以按任何顺序列出，而且这些值都可以忽略。只要提供了一个值，其它的就会填入其默认值。 

注意：实际工作中我们会去掉列表的默认属性

```css
ul { 
    list-style:none; /*去掉列表的默认属性*/
    padding:0; /*去掉列表的默认内边距*/
    margin:0;/*去掉列表的默认外边距*/
}
```

# 表格的样式

| 属性            | 属性值                  | 描述                                     |
| --------------- | ----------------------- | ---------------------------------------- |
| width           | 数值                    | 宽度                                     |
| height          | 数值                    | 高度                                     |
| border          |                         | 边框                                     |
| border-collapse | separate \| collapse    | 设置表格的边框是否被合并为一个单一的边框 |
| border-spacing  | 水平数值 垂直数值       | 相邻单元格的边框间的距离                 |
| padding         | 数值                    | 内容与边框的距离                         |
| text-align      | left \| center \| right | 文本水平对齐方式                         |
| vertical-align  | top \| center \| bottom | 文本垂直对齐方式                         |

## 边框

设置表格的边框（也是设置所有元素的边框）。

语法：

```css
table,th,td { border : 边框宽度 边框样式 边框颜色 ;}
```

案例：

```css
table { border:1px solid #ddd ;}
```

## 折叠边框

设置表格的边框是否被合并为一个单一的边框。

语法：

```css
table { border-collapse : separate | collapse ;}
```

属性值：

separate

collapse

## 边框间距

设置相邻单元格的边框间的距离，等同于表格的"cellspacing"属性。

使用时必须设置边框分离"border-collapse : separate;"。

语法：

```css
table { 
    border-collapse : separate;
    border-spacing : 水平数值 垂直数值 ;
}
```

注意：在实际工作中我们会折叠边框，设置边框间距为0；

```css
table {
    border-collapse: collapse;
    border-spacing: 0; 
}
```
## 内边距

设置表格内容与边框的距离（也是设置所有元素内容与边框的距离）。

语法：

```css
th,td { padding : 数值 ;}
```

## 文本水平对齐

设置单元格内文本水平对齐方式（也是设置其他元素内文本水平对齐方式的属性）。

语法：

```css
th,td { text-align : left | center | right ;}
```

## 文本垂直对齐

设置单元格内文本垂直对齐方式

语法：

```css
th,td { vertical-align : top | middle | bottom ;}
```
# 总结

## 超链接

1.链接的状态

```css
a:link /* 未被访问的链接 */
a:visited /* 已被访问的链接 */
a:hover /* 鼠标指针移动到链接上 */
a:active /* 正在被点击的链接 */
```

2.伪类选择器的使用情况

情况一：超链接使用伪类选择器

```css
a { 
	color:#333;
	text-decoration:none;
}
a:hover {
    color:#f00;
}
```

**注意： IE6只能识别超链接上的伪类**

情况二：其他元素使用伪类选择器（IE6不兼容）

```css
li {
	color:#333;
}
li:hover {
    color:#f00;
}
```

情况三：伪类选择器操作后代选择器（IE6不兼容）

```css
ul {
    display:none;
}
li:hover ul {
    display:block;
}
```

3.鼠标样式

```css
cursor:pointer;/*点击手型*/
```

## 列表样式

实际工作中我们会去掉列表的默认属性

```css
ul,ol,dl,dd {
		/* 实际工作中我们会去掉列表的默认属性 */
		list-style:none;
		padding:0;
		margin:0;
	}
```

## 表格的样式

实际工作我们会折叠边框

```css
table {/* 实际工作使用 */
		border-collapse:collapse;
		border-spacing: 0; 
	}
	th,td {
		vertical-align:top;/* 单元格的文本靠上 */
		vertical-align:bottom;/* 单元格的文本靠下 */
		vertical-align:middle;/* 单元格的文本居中 */
	}
```
