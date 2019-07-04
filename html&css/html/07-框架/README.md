# Html框架
## 课程目标
- 了解框架的作用
- 熟记框架的标签和属性
- 了解框架使用的注意事项
- 掌握框架的应用


## 框架的作用
通过使用框架，可以在同一个浏览器窗口显示不止一个html页面

## 框架集
```
<html>
  <head></head>
  <frameset cols="20%,80%">
    <frame src="frame_a.html"></frame>
    <frame src="frame_a.html"></frame>
  </frameset>
<html>
```
### 框架集frameset
定义如何将窗口分割为框架

**属性**

|属性|属性值|说明|
|--|--|
|cols|像素/百分比|规定框架集中列的数目和尺寸，行和列属性只能使用其中一个|
|rows|像素/百分比|规定框架集中行的数目和尺寸，行和列属性只能使用其中一个|

### 框架frame
定义每个框架中的html页面

**属性**

|属性|属性值|说明|
|--|--|
|src|URL|规定iframe中显示的html文档|
|frameborder|0/1|属性值为“0”可以删除边框|
|name|frame_name|规定frame的名称|
|noresize|noresize|规定frame的大小不能改变|

### 注意事项
1. 不能将`<body></body>`标签与`<frameset></frameset>`标签同时使用
2. `<frameset></frameset>`中`cols`和`rows`只能使用一个
3. 使用`<noframes></noframes>`添加文本时，必须将文字嵌套在`<body></body>`标签内

## 内联框架iframe
用于在网页内显示网页
```
<iframe src="URL"></iframe>
```

**属性**

|属性|属性值|说明|
|--|--|
|src|URL|规定iframe中显示的html文档|
|width|像素/百分比|规定iframe的宽度|
|height|像素/百分比|规定iframe的高度|
|frameborder|0/1|属性值为“0”可以删除边框|
|name|frame_name|规定iframe的名称|
|scrolling|auto/yes/no|规定是否在iframe中显示滚动条|

## 框架的应用
### 导航框架

### 跳转至框架内到锚点

### 混合框架结构

## 作业