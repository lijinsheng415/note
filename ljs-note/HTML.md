# HTML

**Http协议，超文本传输协议** 是互联网传输的常见协议

一次http事务是由‘HTTP请求’和‘http响应构成’

网址前面的http\://就是表示用http请求页面

css文件都是 style.css

狭义的HTML5就是HTML5结构标签本身

狭义的CSS3：CSS3相关的样式

广义的HTML5：HTML5本身+CSS3+JavaScript

一般html首页文件名都叫做index.html

# HTML基础

- 3C万维网联合会，是万维网的主要国际标准组织，成立于1995年，负责制定Web标准，主要是HTML和CSS。
- 网站：是指在因特网上根据一定的规则，使用HTML等制作的用于展示特定内容的相关网页合集
- 页：是网站?中的一页，需要通过浏览器来阅读。网页是构成网站的基本元素，它通常由图片、链接、文字、声音、视频等元素组成。通常我们看到的网页，常见以.htm或.html后缀结尾的文件，因此将其俗称为HTML文件。
- Html不是一种编程语言而是一种标记语言,标记语言就是由一套标签组成的
- HTML：是指超文本标记语言（Hyper Text Markup Langage），他是描述网页的一种语言。
- 谓的超文本有两层含义：
1. \- 他可以加入图片、声音、动画、多媒体等内容（超越了文本限制）。&#x20;
2. 他可以从一个文件跳转到另一个文件，与世界各地主机的文件链接（超链接文本）

常用的五大浏览器：IE、谷歌、火狐、欧朋、safari

Web标准构成：主要包括结构（Structure）、表现（Pewsentation）、行为（Behavior）三个方面

1. 结构用html
2. 表现用css
3. 行为用scripr

# HTML结构：

```html
<!-- 文档类型声明标签 用最新的html显示网页 !DOCTYPE文档类型声明标签DTD，作用是用哪个HTML
版本显示网页 位于整个网页第一行，每个html文件第一行必须是DTD（DOCUMENT Type Definition,文
档类型声明） -->
<!DOCTYPE html>

<!-- 文档开头 表示文档的开头和结尾，lang属性就是语言：英语是 “en”,中文是”zh-CN” -->
  <html lang="en">

<!-- 页面头部 -->
  <head>
      <!-- <meatr>字符集标签可以通过Charset 属性来规定HTML文档用哪种字符编码”UTF-8”
      是一种万能码 -->
      <meta charset="UTF-8">

      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <!-- 移动端适配标签  -->
      <meta name="viewport"  content="width=device-width, initial-scale=1.0">

      <!-- 浏览器标签显示的标题 -->
      <title>Document</title>

      <!-- 内嵌样式标签 -->
      <style>
      </style>

  <!-- 页面头部结束 -->
  </head>

  <!-- 页面内容开始 -->
  <body>
      <!-- 内嵌式js标签 -->
      <script>
      </script>

  <!-- 页面内容结束 -->
  </body>

  <!-- 文档结束 -->
  </html>
```

&#x20;      Charset 的常用值：GB2312（制作汉语网页，收录了所有汉语字符，一个字占两个字节）、BLG5、GBK、UTF-8（制作有非汉字的网页，一个汉字栈三个字节）

#### HTML5就是html的第五次重大修改

# HTML语法规范：

- 多数都是双标签 少数是单标签
- 标签关系：分为包含关系和并列关系
- 标签属性之间没有顺序之分，属性之间用空格隔开

## 文字标签

```html
<h1>一级标题</h1> 
<h2>二级标题</h2> 
<h3>三级标题</h3> 
<h4>四级标题</h4> 
<h5>五级标题</h5> 
<h6>六级标题</h6>

<p>段落标签 p标签里面文字和文字之间的多个空格、换行会被折叠成一个空格，
文字和标签之间的空格会被忽略</p>

换行标签</br>

<strong>文字加粗常用</strong>       <b>加粗</b>
<em>文字倾斜常用</em>               <i>倾斜</i>
<del>删除线常用</del>               <s>删除线</s>
<ins>下滑线常用</ins>               <u>下划线</u>

<!-- html注释-->  或 Vs快捷键 ctrl+/
```

## 特殊字符

```html
空格      
大于号   >
小于号   <
版权符号 ©
```

## 容器

```html
<div></div> 大盒子 独占一行  
<span></span>  小盒子 行内块 一行可以多个
```

### H5 新增语义化标签

```html
  <header>头部标签</header>

  <nav>导航标签</nav>

  <article>文档的核心文章内容，会被搜索引擎主要抓取</article>

  <section>定义文档某个区域/块级标签，语义比div大 </section>

  <aside>侧边栏标签，文档的非必要相关内容，比如广告等</aside>

  <footer>尾部标签</footer>

  <main>网页核心部分</main>
```

**新增标签IE9以上支持，这些语义化标签主要是针对搜索引擎的,这些新标签可以再页面中使用多次，在IE9中需要把这些元素转换成块级元素，移动端更喜欢使用这些标签**

## 图像标签 img

```html
<img src=“图像地址” alt=“如果图像不能正常显示，显示的文字” 
title=“鼠标放在图像上显示的文字” width=“图片宽度” height=“图片高度” 
broder=“设置图像边框的粗细”>
```

- 属性采取键值对的方式，键="值"
- 宽度高度不用写单位，省略其中一个则是等比例缩放

### 相对路径

相对路径:相对于当前html文件的位置&#x20;

- 同级：直接输入文件名或者输入`  ./  `然后会自动弹出
- 下级路径：`下级文件夹名/文件名`
- 上级路径：`../`

### 绝对路径

绝对路径:指根目录下的绝对位置,一个网址或者从盘符开始的路径

## 超链接标签 a

```html
<a href="" target="">文本或者图片</a>
```

- a(anchor)锚点.
- href跳转目标分为内部链接和外部链接
  - 外部链接：一个网站
  - 内部链接：网站内部页面之间相互的链接
- target目标窗口弹出方式，*helf从当前窗口默认值，* blank新建一个窗口

### 空链接

```html
<a href=“#”>当链接没有确定时先用#或javascript:;代替</a>
<a href=“javascript:;”>当链接没有确定时先用#或javascript:;代替</a>
```

### 下载链接

下载链接：如果href里面地址指向的是exe、zip、rar等格式，会下载这个文件

### 邮件链接

有**mailto** ：的前缀是邮件链接，系统会自动打开email相关的软件

```html
<a href="mailto:XXXX@qq.com">发邮件</a>
```

### 拨打电话

href中包含tel：可以直接拨打电话

```html
<a href="tel:xxxxx">打电话</a>
```

### 锚点链接

锚点链接:快速定位到当前网页中某个位置

```html
<a href=“#目标ID”></a>
```

在目标位置设置`ID`然后把超链接标签的`href`的属性值设置为`#id名`

## 表格标签

```html
<table align="" border="" cellpadding="" cellspacing="" 
width="" height="">
  <thead>
      <caption>表格大标题</caption>
      <tr>
          <th>表头</th>
          <th>表头</th>
      </tr>
  </thead>
  <tbody>
    <tr>
      <td>单元格</td>
      <td>单元格</td>
    </tr>
  </tbody>
</table>
```

### 表格属性

- `align`表格相对周围元素的对其方式：左侧默认：`left` 居中：`center` 右侧对其： `right`
- `border`：给表格加边框默认是0 改成1就是加边框
- `Cellpadding`：表格内容与表格边缘距离 默认是1像素
- `Cellspacing`：单元格之间的空白默认2像素
- `Width`：表格宽
- `height`：表格高

### 子标签

- `caption`：表格的标题，通常写在所有的tr之前
- `<tr>`表示表格的每一行
- `<th></th>`表示一列的标题， 文字加粗 居中
- `<td></td>`表示一个单元格
- 合并单元格：
  - 跨行合并：`rowspan="合并单元格的个数"` 目标单元格是最上面的
  - 跨列合并：`colspan="合并单元格的个数"` 目标单元格是最左面的
- `<thead></thead>`标签标示用来包含表格的头部区域
- `<tbody></tbody>`标签标示用来包含表格的主体区域
- &#x20;`<tfoot></tfoot>`表示用来包含表格的底部

## 列表标签

### 无序列表

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

ul中只能放li ,li中可以放所有元素

### 有序列表

```html
<ol type="A/a/i/I/1" star="" reversed>
  <li></li>
  <li></li>
  <li></li>
</ol>
```

- ol中只能放li li中可以放所有元素
- ol标签由type属性，可以用来设置编号的类型
- 属性值
  - a :表示小写的英文字母编号
  - A：表示大写的英文字母编号
  - i：表示小写的罗马数字编号
  - I：表示大写的罗马数字编号
  - 1：表示数字编号默认
- star属性：属性值必须是一个整数，指定了列表编号的起始值；
- reversed属性：指定列表中的条目是否倒序排列，不需要值直接写一个属性就可以。H5新增属性

### 自定义列表

```html
<dl>
  <dt>表头</dt>
  <dd>项目1</dd>
  <dd>项目2</dd>
  <dd>项目3</dd>
</dl>
```

dl中只能放dt dd, dt dd中可以放所有元素

## 表单标签：是用来收集用户数据并且返回给后台的

- 表单由：表单域，表单控件（表单元素）和提示信息 三个部分组成

```html
form表示整个表单 会把它范围内的表单元素信息提交给服务器
<form action="" method="" name="">
action：地址用于指定接收并处理表单数据的服务器程序的url地址，属性值是url
method：用于设置表单数据的提交方式，其取值为get 或者post
name：用于指定表单的名称，以区分同一页面的多个表单域
  <input type="text">     输入框
  <input type="password"> 密码框
  <input type="radio">    单选框
  <input type="checkbox"> 复选框
  <input type="reset">    重置按钮 点击后恢复到默认状态
  <input type="submit">   定义提交按钮 点击后吧表单数据送给服务器
  <input type="button">   定义按钮，配合js使用
  <button></button>       定义按钮，配合js使用
  <input type="file">     提供文件上传
  <input type="hidden">   定义隐藏的输入字段
  <input type="image">    定义图像形式的提交按钮
</form>

<form action="" method="" name="">
  <input type="text" name="" value="" 
  checked maxlength="" placeholder="" disabled>
  name属性：由用户自定义 主要给后台人员使用
  Value属性：输入的文字直接会在网页内对应得框显示出来，主要给后台人 员使用
  Checked属性：此元素加载时默认就是选中状态,书写值就是根据值来判断选中状态
  Maxlength属性：输入字段中字符的最大数
  placeholder占位的提示信息
  disabled:禁用文本框
  pattern:规定用于验证输入字段的模式，
        于type类型：text，search，url，telephone，email以及pas
     swordpattern属性得值为正则表达式 正则表达式不需要带最外层的两个斜杠 //

</form>
```

所有的表单标签都具有 `name` `value` `checked` 等属性

### label标签

点击文字时在框里出现光标或者选中

- html4：需要给按钮一个ID，然后\<labe for="ID">按钮的文字\</label>

- html5：可以直接写成标签对把按钮包含在里面
  
  ```html
  <form >
    <labe for="one">单选框</label>
    <input type="radio" id="one">  
  
    <labe for="man">男</label>
    <input type="checkbox" name="sex" id="man" value="nan"> 
    <labe for="woman">女</label>
    <input type="checkbox" name="sex" id="woman" value="nv"> 
  <form >
  ```

#### textarea文本域标签：显示一个文本框可以输入大量文字

```html
<textarea cols="100" rows="20">提示文字 可以显示到文本框里面</textarea>
Cols属性 每行可以输入多少个字 以后可以用js代替
Rows属性 可以写多少行 以后可以用js代替
```

### Select: 下拉表单元素

```html
<select>
    <option value="121" Selected >121<option>
    value 用于选中后返回给后台选中的项
    Selected属性可以打开时就默认选择这个选项

</select>
```

## html5新增

### 新增表单类型 input

```html
<input type="email">  限制用户输入类型必须为Email
<input type="url">    输入类型必须为url
<input type="date">   输入类型必须为日期
<input type="time">   输入类型必须为时间类型
<input type="month">  输入类型必须为月类型
<input type="week">   输入类型必须为周类型
<input type="number"> 输入类型必须为数字类型
<input type="tel">    手机号码
<input type="search"> 搜索框
<input type="color">  生成一个颜色选择表单
```

#### 新增表单属性

- required:该属性表示该表单不能为空值required
- placeholder表单的提示信息存在默认值，获取光标将不显示框里的默认文字
- autofocus自动获得焦点autofocus
- autocomplete 是否显示搜索历史值on/off默认是打开的需要放在表单内，同时加上name属性并且成功提交过
- multiple可以同时多选文件提交值multiple

&#x20;datalist控件

datalist控件可以为输入框提供一些备选项，当用户输入的内容与备选项文字相同时，将会智能感应

```html
<input type="text" list="province-list">
  <datalist id="province-list">
    <option value="山东">
    <option value="山西">
    <option value="陕西">
</datalist>
```

### 新增多媒体标签

#### 视频标签

```html
1. <video src="" width="320" height="240" 
autoplay:autoplay controls:controls loop:loop muted:muted> 
抱歉你的浏览器不支持此标签</video>

2.<video width="320" height="240">
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
您的浏览器不支持此标签
</video>

<video src="" autoplay controls >抱歉你的浏览器不支持</video>
```

- autoplay 如果出现该属性，则视频在就绪后马上播放。

- controls 如果出现该属性，则向用户显示控件，比如播放按钮。

- loop播放完是否继续播放继续就是loop

- width设置播放器宽度 不用写单位

- height设置播放器高度

- src视频地址

- poster加载等待的画面图片

- muted静音播放值muted

- preload是否预加载视频 auto预加载 none不预加载
  
  尽量使用mp4格式 多格式同时使用

#### 多媒体标签audio

支持格式 mp3 wav ogg

```html
<audio src="音频地址" >抱歉你的浏览器不支持</audio>

- autoplay音频就绪后马上播放:autoplay
- controls显示播放控件:controls
- loop音频结束时重新播放:loop
- src播放地址
- muted音频静音输出:muted

谷歌浏览器把autoplay属性禁用了
```

# 实用标签

```html
<pre></pre>:用于展示多行代码的标签,里面的所有换行缩进都会保留
<code></code>: 用于展示一行代码的标签
```
