# 课程目标

- 了解Html5的新特性
- 了解浏览器对Html5的支持
- 熟练掌握Html5的语法规范
- 熟练掌握Html5的语义化标签
- 熟练掌握Html5的多媒体标签
- 熟练掌握html5的新表单类型及属性

# 认识Html5

**HTML5 是 W3C 与 WHATWG 合作的结果**，WHATWG 致力于 web 表单和应用程序，而 W3C 专注于 XHTML 2.0。在 2006 年，双方决定进行合作，来创建一个新版本的 HTML。 

## **Html5新特性**

- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素（学习）
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section（学习）
- 新的表单控件，比如 calendar、date、time、email、url、search（学习）

## 与HTML4相比

1. 智能表单，多媒体标签等
2. 提供了一系列的Javascript API如 地理定位、重力感应、硬件访问等。
3. 结合canvas和css3的过渡、转换、动画等开发网页游戏。

## 浏览器支持

最新版本的 Safari、Chrome、Firefox 以及 Opera 支持某些 HTML5 特性。Internet Explorer 9 将支持某些 HTML5 特性。 

| Safari(苹果) | Chrome（谷歌） | Firefox（火狐） | Opera（欧朋） | IE   |
| ------------ | -------------- | --------------- | ------------- | ---- |
| 新版支持     | 新版支持       | 新版支持        | 新版支持      | +9   |

# 语法规范 

基本遵循xhtml的语法规范。

- 标签小写、属性小写

- 双标签闭合，推荐必须闭合，写结束标签

- 单标签闭合，推荐必须闭合，写/

## 基本结构

```html
<!doctype html>
<html>
	<head>
    	<title>网页标题</title>
    </head>
	<body></body>
</html>
```

## 文档类型

```html
<!doctype html>
```

## 语言

声明语言能让浏览器更快的解析我们的网页（不是html5新的属性）

```html
<html lang="zh-cn">
</html>
```

## 标题

HTML5 中` <title>` 元素是必须的，标题名描述了页面的主题: 

```html
<title>网页标题</title>
```

## 样式表

样式表使用简洁的语法格式 ( type 属性不是必须的): 

```html
<link href="demo.css" rel="stylesheet">
```

## JavaScript

使用简洁的语法来载入外部的脚本文件 ( type 属性不是必须的 ): 

```html
<script src="demo.js">
```

## **不支持的标签**

```html
<center></center>
<font></font>
<frameset>
    <frame></frame>
</frameset>
<noframes></noframes>
<u></u>
```

# 语义化标签

**什么是语义化标签：**

所谓语义化标签是要是html标签具备更好的**可读性**，可以清晰传达每个标签所表示的意义，以方便其更好的被处理和解析。 

**语义化标签有什么优势** 

更有利于搜索引擎或者辅助设备的来理解html页面内容。 

**常用语义化标签**：

```html
<nav></nav> <!-- 导航 -->
<header></header> <!-- 头部（页眉） -->
<footer></footer> <!-- 底部（页脚） -->
<section></section> <!-- 区块 -->
<article></article> <!-- 文章 -->
<aside></aside> <!-- 侧边栏 -->
```

# 多媒体标签

| 标签       | 描述                                         |
| ---------- | -------------------------------------------- |
| `<video>`  | 定义视频，比如电影片段或其他视频流。         |
| `<audio>`  | 定义声音，比如音乐或其他音频流。             |
| `<source>` | 定义`<video> `和 `<audio>`的多媒体资源       |
| `<embed>`  | 定义内嵌对象。HTML4 中不赞成，HTML5 中允许。 |
| `<object>` | 定义内嵌对象。                               |

## 视频video

定义视频，比如电影片段或其他视频流。

```html
<video src="demo.mp4" >
    请使用高版本浏览器
</video>
```

提示：可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

**常用属性：**

| 属性     | 值       | 描述                         |
| -------- | -------- | ---------------------------- |
| src      | URL      | 设置播放视频的路径           |
| autoplay | autoplay | 设置自动播放                 |
| controls | controls | 设置使用浏览器提供的播放控件 |
| loop     | loop     | 设置循环播放                 |
| muted    | muted    | 设置默认静音                 |

**支持视频格式：**

| 格式 | MIME-type  | 浏览器支持 |
| ---- | ---------- | ---------- |
| MP4  | video/mp4  | 高版本浏览器都支持 |
| WebM | video/webm | Safari、IE不支持 |
| Ogg  | video/ogg  | Safari、IE不支持 |

## 音频audio

定义声音，比如音乐或其他音频流。

```html
<audio src="demo.mp3">
    请使用高版本浏览器
</audio>
```

提示：可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

**常用属性**：

| 属性     | 值       | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| src      | URL      | 设置播放音频的路径                       |
| controls | controls | 设置使用浏览器提供的播放控件             |
| autoplay | autoplay | 设置自动播放（谷歌和苹果浏览器已经禁用） |
| loop     | loop     | 设置循环播放                             |
| muted    | muted    | 设置默认静音                             |

**支持音频格式**：

| 格式 | MIME-type  | 浏览器支持         |
| ---- | ---------- | ------------------ |
| MP3  | audio/mpeg | 高版本浏览器都支持 |
| Wav  | audio/wav  | IE不支持           |
| Ogg  | audio/ogg  | Safari、IE不支持   |

## 多媒体资源source

定义`<video> `和 `<audio>`的多媒体资源

```html
<video>
    <source src="demo.mp4" type="video/mp4"></source>
    <source src="demo.ogg" type="video/ogg"></source>
	请使用高版本浏览器
</video>
<audio>
    <source src="demo.mp3" type="audio/mpeg"></source>
    <source src="demo.ogg" type="audio/ogg"></source>
	请使用高版本浏览器
</audio>
```

**属性：**

| 属性 | 值        | 描述                       |
| ---- | --------- | -------------------------- |
| src  | URL       | 设置多媒体资源的路径       |
| type | MIME-type | 设置多媒体资源的 MIME 类型 |

## 内嵌内容embed

使用`<embed>`插入网络上的视频

# 表单标签

## 新标签(写表单的时候会使用到的)

**表单分组 fieldset-legend**

表单框 fieldset，表单框标题 legend

```html
<fieldset>
    <legend>
        用户登录
    </legend>
    姓名：<input type="text" />
    <br/>
    密码：<input type="password" />
</fieldset>
```

**输入框下拉 datalist-option**

```html
<input type="text" list="list" />
<datalist id="list">
	<option></option>
	<option></option>
	<option></option>
</datalist>
```

**进度条 progress**

```html
<progress max="100" value="10"></progress>
```

**度量器 meter**

```html
<meter max="512" value="128"></meter>
```

## input类型

| 类型   | 语法                      | 描述                                 |
| ------ | ------------------------- | ------------------------------------ |
| email  | `<input type="email" />`  | 定义email输入框                      |
| url    | `<input type="url" />`    | 定义路径地址输入框                   |
| color  | `<input type="color" />`  | 定义颜色输入框                       |
| number | `<input type="number" />` | 定义数字输入框                       |
| range  | `<input type="range" />`  | 定义数字范围输入框， 显示为滑动条 。 |
| search | `<input type="search" />` | 定义搜索输入框，和单行文本框一样     |
| time   | `<input type="time" />`   | 定义时间选择框                       |
| date   | `<input type="date" />`   | 定义年-月-日选择框                   |
| month  | `<input type="month" />`  | 定义年-月选择框                      |
| week   | `<input type="week" />`   | 定义年-周选择框                      |

**注意：**并不是所有的主流浏览器都支持新的input类型，不过您已经可以在所有主流的浏览器中使用它们了。即使不被支持，仍然可以显示为常规的文本域。

## 表单属性

**min, max，step**

max 属性规定输入域所允许的最大值。 

min 属性规定输入域所允许的最小值。 

step属性规定输入数字的间隔。

适用于以下类型的` <input>` 标签：date pickers、number 以及 range。 

```html
<input type="number" min="10" max="100" step="2" />
```

**必填项 required**	

必填项不能为空

适用于以下类型的 `<input>` 标签：text, search, url, telephone, email, password, date pickers, number, checkbox, radio 以及 file。 

```html
 <input type="text" required="required" />
```

**提示信息 placeholder**

提示（hint），描述输入域所期待的值。 

适用于以下类型的` <input>` 标签：text, search, url, telephone, email 以及 password。 

```html
<input type="text" placeholder="Search W3School" />
```

**自动获取焦点 autofocus**

自动获取焦点

适用于所有 `<input>` 标签的类型。 

```html
<input type="text" autofocus="autofocus" />
```

**多文件上传 multiple** 

输入域中可选择多个值。 

用于以下类型的` <input>` 标签：email 和 file。 

```html
<input type="file" multiple="multiple"/>
```

**`<from>`自动完成 autocomplete**

规定 form 或 input 域应该拥有自动完成功能。 

值：on 开 off 关

适用于 `<form>` 标签，以及以下类型的`<input>`标签：text, search, url, telephone, email, password, datepickers, range 以及 color。 

**自定义验证 pattern**

描述了一个正则表达式用于验证 `<input> `元素的值 

适用于以下类型的 `<input>` 标签: text, search, url, tel, email, 和 password。

```html
<input type="text" pattern="^[0-9]*$" title="请输入数字">
```

```
数字：^[0-9]*$

Email地址：^\w+([-+.]\w+)@\w+([-.]\w+).\w+([-.]\w+)*$ 

域名：a-zA-Z0-9{0,62}(/.a-zA-Z0-9{0,62})+/.? 

手机号码：^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$
```

**关闭验证 novalidate**

规定在提交表单时不应该验证 form 或 input 域 

```html
<form novalidate="novalidate">
    <input type="text" >
</form>
```

**关联表单 form**

规定输入域所属的一个或多个表单 

```html
<form action="" id="form1">
  姓名：<input type="text" name="fname"><br>
  <input type="submit" value="提交">
</form>
爱好: <input type="text" name="lname" form="form1">
```