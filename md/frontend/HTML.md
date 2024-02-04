# HTML&HTML5

## HTML 简介

### 什么是 HTML?

HTML 是用来描述网页的一种语言。

- HTML 指的是超文本标记语言 (Hyper Text Markup Language)
- HTML 不是一种编程语言，而是一种标记语言 (markup language)，用来告诉浏览器如何组织页面
- 标记语言是一套标记标签 (markup tag)
- HTML 使用标记标签来描述网页
- HTML 由一系列的元素(elements)组成

### HTML 元素(HTML element)

HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

![grumpy-cat-small.png](https://cdn.nlark.com/yuque/0/2023/png/29514937/1673180951971-a7a2250b-e053-44f8-a756-135c5b2cc0d1.png#averageHue=%23312e2e&clientId=u4ae8a0aa-fe39-4&from=drop&height=198&id=u69a4c5bd&originHeight=255&originWidth=821&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8330&status=done&style=none&taskId=uf28ef0d3-173a-481c-9900-efca04dcdc5&title=&width=639)

这个段落元素主要包含：

1. 开始标签（Opening tag）：包含元素的名称（本例为 p），被左、右角括号所包围。表示元素从这里开始或者开始起作用 —— 在本例中即段落由此开始。
2. 闭合标签（Closing tag）：与开始标签相似，只是其在元素名之前包含了一个斜杠。这表示着元素的结尾 —— 在本例中即段落在此结束。
3. 内容（Content）：元素的内容是开始标签与结束标签之间的内容，本例中就是所输入的文本本身。
4. 元素（Element）：开始标签、结束标签与内容相结合，便是一个完整的元素。

> 注释：开始标签常被称为开放标签（opening tag），结束标签常称为闭合标签（closing tag）

---

### HTML 标签(HTML tag)

HTML 标记标签通常被称为 HTML 标签 (HTML tag)。

- HTML 标签是由 _**尖括号**_ 包围的关键词，比如 `<html>`
- HTML 标签通常是 _**成对出现**_ 的，比如 `<b>` 和 `</b>`
- 标签对中的第一个标签是 _**开始标签**_ ，第二个标签是 _**结束标签**_
- 开始和结束标签也被称为 _**开放标签**_ 和 _**闭合标签**_

> **备注：** HTML 标签不区分大小写。也就是说，输入标签时既可以使用大写字母也可以使用小写字母。通常大家统一使用小写字母。

### HTML 文档 = 网页

- HTML 文档 _**描述网页**_
- HTML 文档 _**包含 HTML 标签**_ 和纯文本
- HTML 文档也被称为 _**网页**_

Web 浏览器的作用是读取 HTML 文档，并以网页的形式显示出它们。浏览器不会显示 HTML 标签，而是使用标签来解释页面的内容：

```html
<html> 
  <body> 
    <h1>我的第一个标题</h1> 
    <p>我的第一个段落。</p> 
  </body> 
</html> 
```

例子解释

- `<html>` 与 `</html>` 之间的文本描述网页
- `<body>` 与 `</body>` 之间的文本是可见的页面内容
- `<h1>` 与 `</h1>` 之间的文本被显示为标题
- `<p>` 与 `</p>` 之间的文本被显示为段落

---

## HTML 头部(Head)

### HTML `<head>`元素

`<head>`元素包含了所有的头部标签元素。在 `<head>`元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

可以添加在头部区域的元素标签为: `<title>`, `<style>`, `<meta>`, `<link>`, `<script>`, `<noscript>` 和 `<base>`。

### HTML `<title>`元素

`<title>` 标签定义了不同文档的标题。

`<title>` 在 HTML/XHTML 文档中是必需的。

`<title>`元素:

- 定义了浏览器工具栏的标题
- 当网页添加到收藏夹时，显示在收藏夹中的标题
- 显示在搜索引擎结果页面的标题

### HTML `<base>`元素

`<base>` 标签描述了基本的链接地址/链接目标，该标签作为HTML文档中所有的链接标签的默认链接:

```html
<head>
<base href="http://www.runoob.com/images/" target="_blank">
</head>
```

### HTML `<link>`元素

`<link>` 标签定义了文档与外部资源之间的关系。

`<link>` 标签通常用于链接到样式表:

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

### HTML `<style>`元素

`<style>` 标签定义了HTML文档的样式文件引用地址.

在`<style>`元素中你也可以直接添加样式来渲染 HTML 文档:

```html
<head>
<style type="text/css">
body {
    background-color:yellow;
}
p {
    color:blue
}
</style>
</head>
```

### HTML `<meta>`元素

`<meta>` 标签提供了基本的元数据.元数据也不显示在页面上，但会被浏览器解析。

META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。

### HTML`<script>`元素

`<script>`标签用于加载脚本文件，如： JavaScript。

| 标签 | 描述 |
| --- | --- |
| `<head>` | 定义了文档的信息 |
| `<title>` | 定义了文档的标题 |
| `<base>` | 定义了页面链接标签的默认链接地址 |
| `<link>` | 定义了一个文档和外部资源之间的关系 |
| `<meta>` | 定义了HTML文档中的元数据 |
| `<script>` | 定义了客户端的脚本文件 |
| `<style>` | 定义了HTML文档的样式文件 |

---

## 标题元素(Heading)

HTML 标题（Heading）是通过 `<h1> - <h6>` 等标签进行定义的。

`<h></h>`之间的文本为一个段落。

重要性递减，标题文本全都加粗，字号也会依次减小。

一个标题独占一行。

标题元素包含的文本被浏览器渲染为“块”(block)，标题上下自动添加空白（white space）。

| 标签 | 描述 |
| --- | --- |
| `<html>` | 定义 HTML 文档 |
| `<body>` | 定义文档的主体 |
| `<h1> - <h6>` | 定义 HTML 标题 |
| `<!--...-->` | 定义注释 |

---

## 段落元素(Paragraph)

HTML 段落是通过 `<p>` 标签进行定义的。

`<p></p>`之间的文本为一个段落，上下各显示一个空行。

段落元素是将一些句子或文本组织在一起的块级元素。

| 标签 | 描述 |
| --- | --- |
| `<p>` | 定义一个段落 |

---

## 换行和水平标尺

### 1.换行元素

换行元素造成浏览器跳到下一行显示下一个元素或文本。

换行标记单独使用，编码成`<br>`。

### 2.水平标尺元素

水平标尺元素`<hr>`在网页上配置一条水平线。

水平标尺元素不包含任何文本，编码成void元素，不会单独使用。

| 标签 | 描述 |
| --- | --- |
| `<br>` | 插入单个折行（换行） |
| `<hr>` | 定义水平线 |

---

## 块引用元素

“为网页添加引文”。

`<blockquote>`标记以特殊方式显示引文块——左右两边都缩进。

引文块包含在`<blockquote>`和`</blockquote>`标记之间。

---

## 短语元素

### HTML 文本格式化标签

| 标签 | 描述 |
| --- | --- |
| **`<b>`** | **加粗文本** |
| **`<del>`** | **删除文本** |
| **`<em>`** | **强调文本，倾斜文本，替换`<i>`** |
| **`<i>`** | **倾斜文本** |
| **`<ins>`** | **插入字，下划线** |
| **`<s>`** | **删除文本** |
| **`<small>`** | **小号文本** |
| **`<strong>`** | **强调文本，加粗文本，替换`<b>`** |
| **`<sub>`** | **下标文本** |
| **`<sup>`** | **上标文本** |
| **`<u>`** | **插入字，下划线** |

### HTML "计算机输出" 标签

| 标签 | 描述 |
| --- | --- |
| `<code>` | 代码文本，倾斜 |
| `<kbd>` | 输入文本 |
| `<samp>` | sample文本 |
| `<var>` | 变量文本 |
| `<pre>` | 定义预格式文本 |
| `<mark>` | 记号文本 |

### HTML 引文, 引用, 及标签定义

| 标签 | 描述 |
| --- | --- |
| `<abbr>` | 定义缩写 |
| `<address>` | 定义地址 |
| `<bdo>` | 定义文字方向 |
| `<blockquote>` | 定义长的引用 |
| `<q>` | 定义短的引用语 |
| `<cite>` | 引用文本，倾斜 |
| `<dfn>` | 定义一个定义项目 |

---

## HTML 列表

### 有序列表

有序列表使用 `<ol>` 标签，每个列表项使用 `<li>` 标签。

列表项目使用数字进行标记。

```html
<ol>
 <li>Coffee</li>
 <li>Milk</li>
</ol>
```

> type 属性：使用 type 属性可以定义不同类型的有序列表。默认情况下用数字进行标记。

- type="A"：大写字母列表
- type="a"：小写字母列表
- type="I"：罗马数字列表
- type="i"：小写罗马数字列表

```html
<h4>大写字母列表：</h4>
<ol type="A">
 <li>Apples</li>
 <li>Bananas</li>
</ol>  

<h4>小写字母列表：</h4>
<ol type="a">
 <li>Apples</li>
 <li>Bananas</li>
</ol>  

<h4>罗马数字列表：</h4>
<ol type="I">
 <li>Apples</li>
 <li>Bananas</li>
</ol>  

<h4>小写罗马数字列表：</h4>
<ol type="i">
 <li>Apples</li>
 <li>Bananas</li>
</ol>
```

### 无序列表

无序列表使用 `<ul>` 标签，每个列表项使用 `<li>` 标签。

此列项目使用粗体圆点（典型的小黑圆圈）进行标记。

```html
<ul>
 <li>Coffee</li>
 <li>Milk</li>
</ul>
```

> 无须列表每一列表项可继续嵌套无序列表。

### 自定义列表

自定义列表不仅仅是一列项目，而是项目及其注释的组合。

- 自定义列表以 `<dl>` 标签开始。
- 每个自定义列表项以 `<dt>` 开始。
- 每个自定义列表项的定义以 `<dd>` 开始。

```html
<h4>一个自定义列表：</h4>
<dl>
  <dt>Coffee</dt>
   <dd>- black hot drink</dd>
  <dt>Milk</dt>
  < dd>- white cold drink</dd>
</dl>
```

| 标签 | 描述 |
| --- | --- |
| `<ol>` | 定义有序列表 |
| `<ul>` | 定义无序列表 |
| `<li>` | 定义列表项 |
| `<dl>` | 定义列表 |
| `<dt>` | 自定义列表项目 |
| `<dd>` | 定义自定列表项的描述 |

---

## 结构性元素（区块）

### HTML 区块元素

大多数 HTML 元素被定义为**块级元素**或**内联元素**。

块级元素在浏览器显示时，通常会以新行来开始（和结束）。

实例: `<h1>, <p>, <ul>, <table>`

### HTML 内联元素

内联元素在显示时通常不会以新行开始。

实例: `<b>, <td>, <a>, <img>`

### HTML `<div>` 元素

HTML `<div>` 元素是块级元素，它可用于组合其他 HTML 元素的容器。

如果与 CSS 一同使用，`<div>` 元素可用于对大的内容块设置样式属性。

`<div>` 元素的另一个常见的用途是文档布局。它取代了使用表格定义布局的老式方法。使用 `<table>` 元素进行文档布局不是表格的正确用法。`<table>` 元素的作用是显示表格化的数据。

### HTML `<span>` 元素

HTML `<span>` 元素是内联元素，可用作文本的容器

当与 CSS 一同使用时，`<span>` 元素可用于为部分文本设置样式属性。

| 标签 | 描述 |
| --- | --- |
| `<div>` | 定义了文档的区域，块级 (block-level) |
| `<span>` | 用来组合文档中的行内元素， 内联元素(inline) |

- `<div>`标签：用来布局，一行只能放一个`<div>`，大盒子。division，表示分割分区。
- `<span>`标签：用来布局，一行可以放多个`<span>`，小盒子。span意为跨度、跨距。
- `<header>`标签：用于包含网页文档或文档区域的标题。
- `<nav>`标签：用于建立一个导航链接区域。
- `<footer>`标签：用于为网页或网页区域创建页脚。

---

## 图像标签(Img)

HTML 图像是通过 `<img>` 标签进行定义的。

1. 图像标签可拥有多个属性，必须写在标签名的后面。
2. 属性之间不分先后顺序，标签名与属性、属性与属性之间均以空格分开。
3. 属性采取键值对的格式，即 key="value"的格式，属性=”属性值“。

| 属性 | 属性值 | 说明 |
| --- | --- | --- |
| src | 图片路径 | 必须属性 |
| alt | 文本 | 替换文本，图形不能显示的文字 |
| title | 文本 | 提示文本，鼠标放到图形上显示的文字 |
| width | 像素 | 设置图像显示的宽度 |
| height | 像素 | 设置图像显示的高度 |
| border | 像素 | 设置图形的边框粗细 |
| `<area>` || 定义图像地图中的可点击区域 |

```html
<img src="" alt="" />
```

---

## 相对路径、绝对路径

> 目录文件夹：就是普通文件夹，里面只不过存放了我们做页面所需要的相关索材，比如html文件、图片等。
> 根目录：打开目录文件夹的第一层就是根目录。

1. 相对路径：`/`
    - 同一级路径：图形文件与HTML文件同一级，`<img src="baidu.gif"/>`。
    - 下一级路径：图形文件位于HTML文件下一级，`<img src="images/baidu.gif"/>`
    - 上一级路径：图形文件位于HTML文件上一级，`<img src="../baidu.gif"/>`

2. 绝对路径：`\`
    - 目录下的绝对位置，直接到达目标位置，通常是从盘符开始的路径。
    - `D:\web\img\logo.gif` 或 `http://www. …… ./images/logo.gif`

---

## 锚元素

HTML 链接是通过 `<a>` 标签进行定义的。两个标记之间是可以点击的链接文本或图片。

> 锚元素（anchor element）的作用是定义超链接，它指向你想显示的一个网页或文件。

### HTML 链接语法

```html
<a href="URL">链接文本</a>
```

**注释：**在 href 属性中指定链接的地址。

- 外部链接：例如`< a href= "http:// <www.baidu.com">百度></a>`。
- 内部链接：网站内部页面之间的相互链接直接链接内部页面名称即可，例如`< a href="index.html">首页</a>`。
- 空链接：如果当时没有确定链接目标时，`<a href="#">首页</a>`
- 下载链接：如果href里面地址是一个文件或者压缩包，会下载这个文件。
- 网页元素链接：在网页中的各种网页元素,如文本、图像、表格、音频、视频等都可以添加超链接。

> ## 基本的注意事项 - 有用的提示
>
> **注释：** 请始终将正斜杠添加到子文件夹。假如这样书写链接：`href="<https://www.runoob.com/html">`，就会向服务器产生两次 HTTP 请求。这是因为服务器会添加正斜杠到这个地址，然后创建一个新的请求，就像这样：`href="<https://www.runoob.com/html/">`

### 1. 链接目标(target)

使用 target 属性定义被链接的文档在何处显示。
target 为打开窗口的方式：

- _self（默认值，当前窗口打开页面）
-_blank（新窗口打开页面）

```html
<a href="URL" target="_self">链接文本</a>
<a href="URL" target="_blank">链接文本</a>
```

### b).绝对链接

绝对链接指定资源在Web上的绝对位置，用绝对链接来链接其他网站上的资源。

```html
<a href="http://jwgl.just.edu.cn:8080/jsxsd/framework/images/index/index_02.png">链接文本</a>
```

### c).相对链接

相对链接用于链接自己网站内部的网页。链接位置相对于当前显示的网页。
不加`http://`，利用相对"同一级""下一级""上一级"来链接。
用”#“来表示空链接。

### d).block anchor

HTML5为锚标记提供了新功能，即 block  anchor，它能将一个或多个元素（包括作为块显示的，比如div，h1 或者段落）配制成链接。

### e).下载链接

下载链接：地址链接的是文件 .exe 或者是 .zip 等压缩包形式。

### f).锚点链接

锚点链接：点击链接可以快速定位到页面中的某个位置。

- 在链接文本的href属性时，设置属性值为“#名字”的形式，如`<a href="#two">第二集</a>`
- 找到目标位置标签，里面添加一个id属性=刚才的名字，如：`<h3 id="two">第二集介绍</h3>`

## 注释和特殊字符

HTML 中的注释以`<!--`开头，以`-->`结束。快捷键：ctrl+/

| 字符 | 实体名称 | 代码 |
| --- | --- | --- |
| " | 引号 | `&quot;` |
| © | 版权符 | `&copy;` |
| & | &符号 | `&amp;` |
| 空格 | 不间断空格 | `&nbsp;` |
| `` | 撇号 | `&rsquo;` |
| —— | 长破折号 |`&mdash;` |
| &#124; | 竖线 | `&#124;` |

---

## 表格标签(Table)

HTML 表格用`<table>`标签来定义。

- 每个表格均有若干行（由`<tr>`标签定义）
- 每行被分割为若干单元格（由`<td>`标签定义）

用法：

```html
<table>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```

### 表格和边框属性(border)

使用边框属性border来显示一个带有边框的表格：

- border="1" -->带有边框
- border="0" -->不带边框（默认情况下不设置border属性时不带边框）

```html
<table border="1">
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```

### HTML 表格表头

表格的表头使用 `<th>` 标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

```html
<table border="1">
   <tr>
        <th>Header 1</th>
        <th>Header 2</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>
```

### 带标题(caption)的表格

```html
<table border="1">
  <caption>Monthly savings</caption>
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
  <tr>
    <td>February</td>
    <td>$50</td>
  </tr>
</table>
```

### 跨行（列）合并单元格

- 跨列合并：colspan="..."
- 跨行合并：rowspan="..."

```html
<h4>单元格跨两列:</h4>
<table border="1">
 <tr>
   <th>Name</th>
   <th colspan="2">Telephone</th>
  <!-- 		 -->
 </tr>
 <tr>
   <td>Bill Gates</td>
   <td>555 77 854</td>
   <td>555 77 855</td>
 </tr>
</table>

<h4>单元格跨两行:</h4>
<table border="1">
 <tr>
   <th>First Name:</th>
   <td>Bill Gates</td>
 </tr>
 <tr>
   <th rowspan="2">Telephone:</th>
   <td>555 77 854</td>
 </tr>
 <tr>
  <!-- 		 -->
   <td>555 77 855</td>
 </tr>
</table>
```

### 单元格边距、间距

- 单元格边距(Cell padding)：cellpadding="..."，单元格内容与其边框之间的空白
- 单元格间距(Cell spacing)：cellspacing="..."，单元格之间的距离

```html
<h4>有单元格边距、单元格间距:</h4>
<table border="1" cellpadding="10" cellspacing="10">
 <tr>
   <td>First</td>
   <td>Row</td>
 </tr>
 <tr>
   <td>Second</td>
   <td>Row</td>
 </tr>
</table>
```

| 标签 | 描述 |
| --- | --- |
| `<table>` | 定义表格 |
| `<th>` | 定义表格的表头 |
| `<tr>` | 定义表格的行 |
| `<td>` | 定义表格单元 |
| `<caption>` | 定义表格标题 |
| `<colgroup>` | 定义表格列的组 |
| `<col>` | 定义用于表格列的属性 |
| `<thead>` | 定义表格的页眉 |
| `<tbody>` | 定义表格的主体 |
| `<tfoot>` | 定义表格的页脚 |

---

## 表单标签(Form)

HTML 表单用于收集用户的输入信息。

HTML 表单表示文档中的一个区域，此区域包含交互控件，将用户收集到的信息发送到 Web 服务器。

| 属性 | 属性值 | 作用 |
| --- | --- | --- |
| action | url地址 | 用于指定接收并处理表单数据的服务器程序的url地址 |
| method | get/post | 用于设置表单数据的提交方式，其取值为get或post |
| name | 名称 | 用于指定表单的名称，以区分同一个页面中的多个表单域 |

- **post**：指的是 HTTP POST 方法，表单数据会包含在表单体内然后发送给服务器，用于提交敏感数据，如用户名与密码等。
- **get**：默认值，指的是 HTTP GET 方法，表单数据会附加在 **action** 属性的 URL 中，并以 **?**作为分隔符，一般用于不敏感信息，如分页等。例如：<https://www.runoob.com/?page=1，这里的> page=1 就是 get 方法提交的数据。

### HTML 表单 - 输入元素

多数情况下被用到的表单标签是输入标签 **`<input>`**。输入类型是由 **type** 属性定义。

#### 输入类型

| 类型 | 说明 | 注意 |
| --- | --- | --- |
| text | 文本域（Text Fields） | 在大多数浏览器中，文本域的默认宽度是 20 个字符。 |
| password | 密码字段 | 密码字段字符不会明文显示，而是以星号 ***** 或圆点**.** 替代。 |
| radio | 单选按钮（Radio Buttons） |
 |
| checkbox | 复选框（Checkboxes） |
 |
| submit | 提交按钮(Submit) |
 |
| select | 下拉列表 |
 |
| reset | 重置 |  |

> checked 属性定义单选按钮与复选框的预选值。

#### 文本域

文本域使用 `<textarea>` 标签

- rows 属性：定义文本域高度
- cols 属性：定义文本域宽度

```html
<textarea rows="10" cols="30">
我是一个文本框。
</textarea>
```

#### 提交按钮(Submit)

当用户单击确认按钮时，表单的内容会被传送到服务器。表单的动作属性 **action** 定义了服务端的文件名。

#### 下拉列表

下拉列表使用 `<select>` 标签，每个列表项使用 `<option>` 标签。

selected 属性创建预选值。

```html
<form action="">
 <select name="cars">
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="fiat" selected>Fiat</option>
  <option value="audi">Audi</option>
 </select>
</form>
```

HTML5 新标签：

| 标签 | 描述 |
| --- | --- |
| `<form>` | 定义供用户输入的表单 |
| `<input>` | 定义输入域 |
| `<textarea>` | 定义文本域 (一个多行的输入控件) |
| `<label>` | 定义了 `<input>` 元素的标签，一般为输入标题 |
| `<fieldset>` | 定义了一组相关的表单元素，并使用外框包含起来 |
| `<legend>` | 定义了 `<fieldset>` 元素的标题 |
| `<select>` | 定义了下拉选项列表 |
| `<optgroup>` | 定义选项组 |
| `<option>` | 定义下拉列表中的选项 |
| `<button>` | 定义一个点击按钮 |
| `<datalist>` **New** | 指定一个预先定义的输入控件选项列表 |
| `<keygen>` **New** | 定义了表单的密钥对生成器字段 |
| `<output>` **New** | 定义一个计算结果 |

---

## HTML 框架

使用框架可以在同一个浏览器窗口中显示不止一个页面。

**iframe语法:**`<iframe src="URL"></iframe>`

### iframe - 设置高度与宽度

height 和 width 属性用来定义iframe标签的高度与宽度。

属性默认以像素为单位, 但是你可以指定其按比例显示 (如："80%")。

```html
<iframe loading="lazy" src="demo_iframe.htm" width="200" height="200"></iframe>
```

### iframe-移除边框

frameborder 属性用于定义iframe表示是否显示边框。

设置属性值为 "0" 移除iframe的边框:

```html
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```

### iframe目标链接页面

iframe 可以显示一个目标链接的页面，目标链接的属性必须使用 iframe 的属性

```html
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="https://www.runoob.com" target="iframe_a" rel="noopener">RUNOOB.COM</a></p>
```

| 标签 | 说明 |
| --- | --- |
| `<iframe>` | 定义一个内联的iframe |

---

## HTML 脚本

### HTML `<script>` 标签

`<script>` 标签用于定义客户端脚本，比如 JavaScript。

`<script>` 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。

### HTML`<noscript>` 标签

`<noscript>` 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。

`<noscript>`元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

只有在浏览器不支持脚本或者禁用脚本时，才会显示 `<noscript>` 元素中的内容：

```html
<script>
document.write("Hello World!")
</script>
<noscript>抱歉，你的浏览器不支持 JavaScript!</noscript>
```

| 标签 | 描述 |
| --- | --- |
| `<script>` | 定义了客户端脚本 |
| `<noscript>` | 定义了不支持脚本浏览器输出的文本 |

---
