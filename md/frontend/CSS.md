# CSS & CSS3

## CSS 简介

- CSS 指层叠样式表 (**C**ascading **S**tyle **S**heets)
- 样式定义**如何显示** HTML 元素
- 样式通常存储在**样式表**中
- 把样式添加到 HTML 4.0 中，是为了**解决内容与表现分离的问题**
- **外部样式表**可以极大提高工作效率
- 外部样式表通常存储在 **CSS 文件**中
- 多个样式定义可**层叠**为一个

---

## CSS 语法

CSS规则由两个主要的部分构成：选择器、以及一条或多条声明。

![632877C9-2462-41D6-BD0E-F7317E4C42AC.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/29514937/1673491145698-1ec0e408-1d17-45b7-9c92-9ed9bbdca420.jpeg#averageHue=%23a3c44b&clientId=u88524407-e0b2-4&from=drop&height=119&id=u5f09e646&originHeight=120&originWidth=570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20085&status=done&style=none&taskId=u80756826-b56e-4db5-ac64-f8baa24f0a3&title=&width=567)

- 选择器是用于指定 CSS 样式的 HTML 标签，花括号内是对该对象设置的具体样式
- 属性和属性值以“键值对”的形式出现，它们之间用英文“:”分开
- 属性是对指定的对象设置的样式属性，例如字体大小、文本颜色等
- 多个“键值对”之间用英文“;”进行区分  

> CSS注释以 **/*** 开始, 以 ***/** 结束

---

## Emmet 语法

### 1、快速生成html标签

1. 生成标签直接输入标签名按tab键即可，比如 div 然后tab键，就可以生成`<div></div>`
2. 如果想要生成多个相同标签加上*就可以了，比如 div*3 就可以快速生成3个div
3. 如果有父子级关系的标签,可以用>，比如ul > li就可以了
4. 如果有兄弟关系的标签，用+就可以了，比如div+p
5. 如果生成带有类名或者id名字的，直接写.demo或者#two tab 键就可以了
6. 如果生成的 div 类名是有顺序的，可以用自增符号$
7. 如果想要在生成的标签内部写内容可以用 () 表示

### 2、快速生成css样式

CSS基本采取简写形式即可：

1. 比如 w200 按 Tab 可以生成 width:200px;
2. 比如 lh26 按 Tab 可以生成 line-height: 26px;

### 3、快速格式化代码

Vscode快速格式化代码: shift+ alt+f

**也可以设置当我们保存页面的时候自动格式化代码:**

1. 文件---> [首选项] ---> [设置] ;
2. 搜索emmet.include;
3. 在settings.json下的【用户】中添加以下语句：

- "editor.formatOnType*:true,
- "editor.formatOnSave*:true

只需要设置一次即可，以后都可以自动保存格式化代码。

---

## CSS 引入方式

### 行内样式表(Inline style)

 行内样式表（内联样式表）是在元素标签内部的 style 属性中设定 CSS 样式。适合于修改简单样式。

```css
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

### 内部样式表(Internal style sheet)

内部样式表（内嵌样式表）是写到 html 文档头部，是将所有的 CSS 代码抽取出来，单独放到一个`<style>`标签内部。

```css
<head>
 <style>
  hr {
   color:sienna;
  }
  p {
   margin-left:20px;
  }
  body {
   background-image:url("images/back40.gif");
  }
 </style>
</head>
```

### 外部样式表(External style sheet)

每个页面使用 `<link>` 标签链接到样式表。 `<link>` 标签在（文档的）头部：

```css
<head>
 <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

### 多重样式优先级

样式表允许以多种方式规定样式信息。样式可以规定在单个的 HTML 元素中，在 HTML 页的头元素中，或在一个外部的 CSS 文件中。甚至可以在同一个 HTML 文档内部引用多个外部样式表。

一般情况下，优先级如下：
**（内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式**

### 优先级顺序

下列是一份优先级**逐级增加**的选择器列表：

- 通用选择器（*）
- 元素(类型)选择器
- 类选择器
- 属性选择器
- 伪类
- ID 选择器
- 内联样式

---

## CSS 基础选择器

> 选择器（选择符）就是根据不同需求把不同的标签选出来这就是选择器的作用。 简单来说，就是选择标签用的。  

### 1、标签选择器

 标签选择器（元素选择器）是指用 HTML 标签名称 作为选择器，按标签名称分类，为页面中某一类标签指定统一的 CSS 样式。

```css
/* 标签选择器 : 写上标签名 */
p {
    color: green;
}
div {
    color: pink;
}
```

### 2、id 选择器

 id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。

```css

<head>
 <style>
  #nav {
    color:red;
  }
 </style>
</head>

/* 结构需要用 id 属性来调用 id 的意思 */
<div id="nav"> 变红色 </div>
```

> **注意：**
>
> - id 属性只能在每个 HTML 文档中出现一次。
> - id 属性不要以数字开头，数字开头的 id 在 Mozilla/Firefox 浏览器中不起作用。

### 3、class 选择器

class 选择器用于差异化选择不同的标签，单独选一个或者某几个标签。

```html
<head>
 <style>
  .red {
   color: red;
  }
 </style>
</head>

/* 结构需要用 class 属性来调用 class 类的意思 */
<div class="red"> 变红色 </div>
```

> **注意：**类名的第一个字符不能使用数字，它无法在 Mozilla/Firefox 浏览器中起作用。

### 4、类选择器-多类名

 多类名使用方式 ：`<div class="red fontSize">多类名</div>`

- 在标签class 属性中写多个类名
- 多个类名中间必须用空格分开
- 这个标签就可以分别具有这些类名的样式  

### 5、通配符选择器

 在 CSS 中，通配符选择器使用“*”定义，它表示选取页面中所有元素（标签）。  

```css
* {
 margin: 0;
 padding: 0;
}
```

---

## CSS Backgrounds(背景)

CSS 属性定义背景效果:

- background-image
- background-repeat
- background-attachment
- background-position

| Property | 描述 |
| --- | --- |
| background | 简写属性，作用是将背景属性设置在一个声明中。 |
| background-attachment | 背景图像是否固定或者随着页面的其余部分滚动。

- 固定：background-attachment : fixed;
 |
| background-color | 设置元素的背景颜色。 |
| background-image | 把图像设置为背景。(默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体) |
| background-position | 设置背景图像的起始位置。 |
| background-repeat | 设置背景图像是否及如何重复。 |

### 背景颜色

background-color 属性定义了元素的背景颜色

CSS中，颜色值通常以以下方式定义：

- 十六进制 - 如："#ff0000"
- RGB - 如："rgb(255,0,0)"
- 颜色名称 - 如："red"

```css
h1 {background-color:#6495ed;}
p {background-color:#e0ffff;}
div {background-color:#b0c4de;}
```

### 背景图像

background-image 属性描述了元素的背景图像

默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体

```css
body {background-image:url('paper.gif');}
```

### 水平或垂直平铺/不平铺

background-repeat 属性规定背景图像在页面的水平或者垂直方向平铺。

- 图像在水平方向平铺 (repeat-x)：

```css
body {
 background-image:url('gradient2.png');
 background-repeat:repeat-x;
}
```

- 图像在垂直方向平铺 (repeat-y)：

```css
body {
 background-image:url('gradient2.png');
 background-repeat:repeat-y;
}
```

- 图像不平铺 (no-repeat)：

```css
body {
 background-image:url('gradient2.png');
 background-repeat:no-repeat;
}
```

### 背景图像- 设置定位

background-position 属性改变图像在背景中的位置：

```css
body {
 background-image:url('img_tree.png');
 background-repeat:no-repeat;
 background-position:right top;
}
```

### 背景- 简写属性

实际开发中页面的背景颜色将由通过很多的属性来控制。
为了简化这些属性的代码，我们可以将这些属性合并在同一个属性中。

背景颜色的简写属性为 "background"：

```css
body {
 background:#ffffff url('img_tree.png') no-repeat right top;
}
```

> 当使用简写属性时，属性值的顺序为：
>
> - background-color
> - background-image
> - background-repeat
> - background-attachment
> - background-position

---

## CSS Fonts(字体)

| Property | 描述 |
| --- | --- |
| font | 在一个声明中设置所有的字体属性 |
| font-family | 指定文本的字体系列 |
| font-size | 指定文本的字体大小 |
| font-style | 指定文本的字体样式 |
| font-variant | 以小型大写字体或者正常字体显示文本。 |
| font-weight | 指定字体的粗细。 |

### 字型

在CSS中，有两种类型的字体系列名称：

- **通用字体系列** - 拥有相似外观的字体系统组合（如 "Serif" 或 "Monospace"）
- **特定字体系列** - 一个特定的字体系列（如 "Times" 或 "Courier"）

| Generic family | 字体系列 | 说明 |
| --- | --- | --- |
| Serif | Times New Roman
Georgia | Serif字体中字符在行的末端拥有额外的装饰 |
| Sans-serif | Arial
Verdana | "Sans"是指无 - 这些字体在末端没有额外的装饰 |
| Monospace | Courier New
Lucida Console | 所有的等宽字符具有相同的宽度 |

### 字体系列

font-family 属性定义文本的字体系列：

- 各种字体之间必须使用英文状态下的逗号隔开
- 一般情况下，如果有空格隔开的多个单词组成的字体，加引号
- 尽量使用系统默认自带字体，保证在任何用户的浏览器中都能正确显示
- 尽量设置几个字体名称作为一种"后备"机制，如果浏览器不支持第一种字体，他将尝试下一种字体。
- 最常见的几个字体："Microsoft YaHei", tahoma, arial, "Hiragino Sans GB";

```css
p { font-family:"微软雅黑";} 
div {font-family: Arial,"Microsoft Yahei", "微软雅黑";}
```

### 字体大小

font-size 属性定义字体大小：

- px（像素）大小是我们网页的最常用的单位（谷歌浏览器默认文字大小为16px）
- 不同浏览器可能默认显示的字号大小不一致，我们尽量给一个明确值大小，不要默认大小
- 可以给 body 指定整个页面文字的大小

字体大小的值可以是绝对或相对的大小：

- 绝对大小：
  - 设置一个指定大小的文本
  - 不允许用户在所有浏览器中改变文本大小
  - 确定了输出的物理尺寸时绝对大小很有用

```css
p { 
 font-size: 20px; 
}
```

- 相对大小：
  - 相对于周围的元素来设置大小
  - 允许用户在浏览器中改变文字大小
  - 1em的默认大小是16px，像素转换为 em 公式：**px/16=em**

```css
/* 40px/16=2.5em */
h1 {
 font-size:2.5em;
} 
```

### 字体粗细

font-weight 属性设置文本字体的粗细：

- normal：默认值（不加粗的）
- lighter：定义细体
- blod：定义粗体（加粗的）
- 100-900：400等同于normal，而700等同于bold，注意这个数字后面不跟单位

```css
p { 
 font-weight: bold;
}
```

### 字体样式

font-style 属性设置文本的风格：

- normal：默认值，正常显示文本
- italic：以斜体字显示的文字
- oblique：文字向一边倾斜（和斜体非常类似，但不太支持）

```css
p { 
 font-style: normal;
}
```

### 字体转变

font-variant 属性设置文本字体的转变：

- normal：默认值（不加粗的）
- small-caps：显示小型大写字母

```css
p { 
 font-variant: normal;
}
```

### 字体复合属性

 字体属性可以把以上文字样式综合来写, 这样可以更节约代码：

- 使用 font 属性时，必须按上面语法格式中的顺序书写，不能更换顺序，并且各个属性间以空格隔开
- 不需要设置的属性可以省略（取默认值），但必须保留 font-size 和 font-family 属性，否则 font 属性将不起作用

```css
/* font: font-style  font-weight  font-size/line-height  font-family; */
font: italic 700 16px 'Microsoft yahei';
```

---

## CSS Link(链接)

### 1.链接状态

特别的链接，可以有不同的样式，这取决于他们是什么状态。

这四个链接状态是：

- a : link - 正常，未访问过的链接
- a : visited - 用户已访问过的链接
- a : hover - 当用户鼠标放在链接上时
- a : active - 链接被点击的那一刻

```css
a:link { color:#000000; }/* 未访问链接*/
a:visited { color:#00FF00; }/* 已访问链接 */
a:hover { color:#FF00FF; }/* 鼠标移动到链接上 */
a:active { color:#0000FF; }/* 鼠标点击时 */
```

当设置为若干链路状态的样式，也有一些顺序规则：

- a : hover 必须跟在 a : link 和 a : visited后面
- a : active 必须跟在 a : hover后面

### 2.文本修饰

text-decoration 属性主要用于删除链接中的下划线：

```css
a:link{text-decoration:none;}
a:visited{text-decoration:none;}
a:hover{text-decoration:underline;}
a:active{text-decoration:underline;}
```

### 3.背景颜色

background-color 属性指定链接背景色：

```css
a:link{background-color:#B2FF99;}
a:visited{background-color:#FFFF85;}
a:hover{background-color:#FF704D;}
a:active{background-color:#FF704D;}
```

---

## CSS 列表

| 属性 | 描述 |
| --- | --- |
| list-style | 简写属性。用于把所有用于列表的属性设置于一个声明中 |
| list-style-image | 将图像设置为列表项标志。 |
| list-style-position | 设置列表中列表项标志的位置。 |
| list-style-type | 设置列表项标志的类型。 |

在 HTML中，有两种类型的列表：

- 无序列表 **ul** - 列表项标记用特殊图形（如小黑点、小方框等）
- 有序列表 **ol** - 列表项的标记有数字或字母

使用 CSS，可以列出进一步的样式，并可用图像作列表项标记。

### 不同的列表项标记

list-style-type 属性指定列表项标记的类型是：

- circle：
- square：
- upper-roman：
- lower-alpha：

```css
ul.a{list-style-type:circle;}
ol.b{list-style-type:lower-alpha;}
```

### 作为列表项标记的图像

list-style-image 属性可图像作为指定列表项标记：

```css
ul { 
 list-style-image:url('sqpurple.gif');
}
```

**注意：**
上面的例子在所有浏览器中显示并不相同，IE 和 Opera 显示图像标记比火狐，Chrome 和 Safari更高一点点。
如果你想在所有的浏览器放置同样的形象标志，就应使用浏览器兼容性解决方案，过程如下：

#### 浏览器兼容性解决方案

同样在所有的浏览器，下面的例子会显示的图像标记：

```css
ul { 
 list-style-type:none; 
 padding:0px; 
 margin:0px; 
}
ul li { 
 background-image:url(sqpurple.gif); 
 background-repeat:no-repeat; 
 background-position:0px5px; 
 padding-left:14px;
}
```

例子解释：

- ul:
  - 设置列表类型为没有列表项标记
  - 设置填充和边距 0px（浏览器兼容性）
- ul 中所有 li:
  - 设置图像的 URL，并设置它只显示一次（无重复）
  - 您需要的定位图像位置（左 0px 和上下 5px）
  - 用 padding-left 属性把文本置于列表中

### 移除默认设置

list-style-type : none 属性可以用于移除小标记。
默认情况下列表`<ul>`或 `<ol>` 还设置了内边距和外边距，可使用 margin : 0 和 padding : 0 来移除:

```css
ul { 
 list-style-type:none; 
 margin:0; 
 padding:0; 
}
```

### 列表 - 简写属性

为列表使用简写属性，按顺序设置如下属性：

- list-style-type
- list-style-position
- list-style-image

如果上述值丢失一个，其余仍在指定的顺序，就没关系。

```css
ul { 
 list-style:squareurl("sqpurple.gif"); 
}
```

---

## CSS Table(表格)

### 表格边框

border属性用于指定CSS表格边框：

```css
table, th, td {
    border: 1px solid black;
}
```

### 折叠边框

border-collapse 属性设置表格的边框是否被折叠成一个单一的边框或隔开：

```css
table {
    border-collapse:collapse;
}
table,th, td {
    border: 1px solid black;
}
```

### 表格宽度和高度

Width 和 height 属性定义表格的宽度和高度：

```css
/* 设置100％的宽度，50像素的th元素的高度的表格： */
table {
    width:100%;
}
th {
    height:50px;
}
```

### 表格文字对齐

表格中的文本对齐和垂直对齐属性。
text-align属性设置水平对齐方式，向左，右，或中心：

```css
td {
    text-align:right;
}
```

垂直对齐属性设置垂直对齐，比如顶部，底部或中间：

```css
td {
    height:50px;
    vertical-align:bottom;
}
```

### 表格填充

如需控制边框和表格内容之间的间距，应使用td和th元素的填充属性：

```css
td {
    padding:15px;
}
```

### 表格颜色

下面的例子指定边框的颜色，和th元素的文本和背景颜色：

```css
table, td, th {
    border:1px solid green;
}
th {
    background-color:green;
    color:white;
}
```

### 定位表格标题

caption-side定位表格标题：

```css
caption {
  caption-side:bottom;
}
```

---

## CSS Text(文本)

| 属性 | 描述 | 注意 |
| --- | --- | --- |
| color | 设置文本颜色 | 通常用十六进制，而且是#fff |
| direction | 设置文本方向。 |

- 默认书写方向
- direction : rtl --> 从右到左的书写方向
 |
| letter-spacing | 设置字符间距 | 增加或减少字符之间的空间 (单位 px) |
| line-height | 设置行高 | 控制行与行之间的距离  |
| text-align | 对齐元素中的文本 | 可以设定文字水平的对齐方式 |
| text-decoration | 向文本添加修饰 | 添加下划线underline，取消下划线none |
| text-indent | 缩进元素中文本的首行 | 通常应用于段落首行缩进2个字的距离text-indent: 2em； |
| text-shadow | 设置文本阴影 | text-shadow : 2px 2px #FF0000 ; |
| text-transform | 控制元素中的字母 |
 |
| unicode-bidi | 设置或返回文本是否被重写  |
 |
| vertical-align | 设置元素的垂直对齐 |
- text-top 对齐
- text-bottom 对齐
 |
| white-space | 设置元素中空白的处理方式 | 禁用文字环绕：white-space : nowrap; |
| word-spacing | 设置字间距 |
 |

### 文本颜色

 color 属性用于定义文本的颜色：

- 十六进制值 - - 如: **＃FF0000、#FF6600，#29D794**
- RGB代码 - - 如: **RGB(255,0,0)、rgb(255,0,0)或rgb(100%,0%,0%)**
- 预定义的颜色值 - - 如: **red**

> 十六进制中相连的两个数字或字母相同，可只写一个。例：#FF0000可写成#F00

```css
div { 
 color: red;
}
```

### 文本对齐

 text-align 属性用于设置元素内文本内容的水平对齐方式：

- left：左对齐（默认值）
- right：右对齐
- center：居中对齐
- justify：两端对齐

```css
div {
 text-align: left;
 ...
}
```

### 文本装饰

 text-decoration 属性规定添加到文本的修饰：

- none：默认，没有装饰线（最常用，用于删除链接的下划线）
- underline：下划线，链接 a 自带下划线（常用）
- overline：上划线（几乎不用）
- line-through：删除线（不常用）

```css
div {
 text-decoration：underline；
 ...
}
```

### 文本转换

text-transform 属性是用来指定在一个文本中的大写和小写字母：

- uppercase：所有字句变成大写字母
- lowercase：所有字句变成小写字母
- capitalize：所有字句变成每个单词的首字母大写

```css
p.uppercase {
 text-transform:uppercase;
}
p.lowercase {
 text-transform:lowercase;
}
p.capitalize {
 text-transform:capitalize;
}
```

### 文本缩进

 text-indent 属性用来指定文本的第一行的缩进，通常是将段落的首行缩进。  

```css
/* 文本的第一行首行缩进 多少距离  */
text-indent: 20px;
/* 如果此时写了2em 则是缩进当前元素 2 个文字大小的距离  */
text-indent: 2em;  
```

- 通过设置该属性，所有元素的第一行都可以缩进一个给定的长度，甚至该长度可以是负值。  
- em 是一个相对单位，就是当前元素（font-size) 1 个文字的大小，如果当前元素没有设置大小，则会按照父元素的 1 个文字大小。  

### 行间距

line-height 属性用于设置行间的距离(行高)：

- line-height : 26px
- line-height : 200% --> 大多数浏览器的默认行高约为110%至120%

![J1[WQY$*53U)N66@E*_[1HQ.png](https://cdn.nlark.com/yuque/0/2022/png/29514937/1666951154941-5201549b-a0ac-4178-bbcb-9471eb949f81.png#averageHue=%23464a3d&clientId=ua5ced100-2fba-4&from=drop&height=183&id=ucb233fee&originHeight=207&originWidth=603&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21795&status=done&style=none&taskId=u4d2eda71-1c63-4cd7-ae99-c6958f74fd5&title=&width=534)

```css
p {
 line-height: 26px;
 line-height:200%;
}
```

---

## CSS 复合选择器

> 复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的，可以更准确、更高效的选择目标元素（标签）

### 后代选择器 (重要）

后代选择器又称为包含选择器，可以选择父元素里面子元素。
其写法就是把外层标签写在前面，内层标签写在后面，**中间用空格分隔**。当标签发生嵌套时，内层标签就成为外层标签的后代。

上述语法表示**选择元素 1 里面的所有元素 2** (后代元素)。

**语法说明**：

- 元素1 和 元素2 中间用空格隔开
- 元素1 是父级，元素2 是子级，最终选择的是元素2
- 元素2 可以是儿子，也可以是孙子等，只要是元素1 的后代即可
- 元素1 和 元素2 可以是任意基础选择器

**实例：**选取所有 `<p>` 元素插入到 `<div>` 元素中:

```html
<html>
 <head>
  <style>
   div p
   {
    background-color:yellow;
   }
  </style>
 </head>
 <body>
  <div>
   <p>段落 1。 在 div 中。</p>
   <p>段落 2。 在 div 中。</p>
  </div>

  <p>段落 3。不在 div 中。</p>
  <p>段落 4。不在 div 中。</p>
 </body>
</html>
```

### 子选择器 (重要）

子元素选择器（Child selectors）只能选择作为某元素的最近一级子元素（简单理解就是选亲儿子元素）
其写法就是子元素选择器(以大于 **>** 号分隔）

上述语法表示**选择元素1 里面的所有直接后代(子元素) 元素2**。

语法说明：

- 元素1 和 元素2 中间用 大于号 隔开
- 元素1 是父级，元素2 是子级，最终选择的是元素2
- 元素2 必须是亲儿子，其孙子、重孙之类都不归他管. 你也可以叫他 亲儿子选择器

```html
<html>
 <head>
  <style>
   div>p
   {
    background-color:yellow;
   }
  </style>
 </head>
 <body>
  <h1>Welcome to My Homepage</h1>
  <div>
   <h2>My name is Donald</h2>
   <p>I live in Duckburg.</p>
  </div>

  <div>
   <span><p>I will not be styled.</p></span>
  </div>

  <p>My best friend is Mickey.</p>
 </body>
</html>
```

### 并集选择器 (重要）

并集选择器可以选择多组标签, 同时为他们定义相同的样式，通常用于集体声明。并集选择器是各选择器通过英文逗号（,）连接而成，任何形式的选择器都可以作为并集选择器的一部分。

上述语法表示选择元素1 和 元素2。

语法说明：

- 元素1 和 元素2 中间用逗号隔开
- 逗号可以理解为和的意思
- 并集选择器通常用于集体声明

### 伪类选择器

伪类选择器用于向某些选择器添加特殊的效果，比如给链接添加特殊效果，或选择第1个，第n个元素。

伪类选择器书写最大的特点是用冒号（:）表示，比如 :hover 、 :first-child 。

### 链接伪类选择器

伪类选择器用于向某些选择器添加特殊的效果，比如给链接添加特殊效果，或选择第1个，第n个元素。

伪类选择器书写最大的特点是用冒号（:）表示，比如 :hover 、 :first-child 。

  a:link 没有点击过的(访问过的)链接
  a:visited 点击过的(访问过的)链接
  a:hover 鼠标经过的那个链接
  a:active 鼠标正在按下还没有弹起鼠标的那个链接

链接伪类选择器注意事项

  为了确保生效，请按照 LVHA 的循顺序声明 :link－:visited－:hover－:active。

  记忆法：love hate 或者 lv 包包 hao 。

  因为 a 链接在浏览器中具有默认样式，所以我们实际工作中都需要给链接单独指定样式。

链接伪类选择器实际工作开发中的写法：

### :focus 伪类选择器

  :focus 伪类选择器用于选取获得焦点的表单元素。

  焦点就是光标，一般情况  类表单元素才能获取

---

## CSS Display(显示)

### 什么是元素的显示模式

**定义：**元素显示模式就是元素（标签）以什么方式进行显示

**作用：**网页的标签非常多，在不同地方会用到不同类型的标签，了解他们的特点可以更好的布局我们的网页。

### 元素显示模式的分类

#### 块元素

**常见的块元素**：

```md
<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>
```

**块级元素的特点**：

- 比较霸道，自己独占一行。
- 高度，宽度、外边距以及内边距都可以控制。
- 宽度默认是容器（父级宽度）的100%。
- 是一个容器及盒子，里面可以放行内或者块级元素。

**注意：** 文字类的元素内不能放块级元素

```md
<p> 标签主要用于存放文字，因此 <p> 里面不能放块级元素，特别是不能放<div> 
同理， <h1>~<h6>等都是文字类块级标签，里面也不能放其他块级元素
```

#### 行内元素

**常见的行内元素：**

```md
<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>
```

标签是最典型的行内元素。有的地方也将行内元素称为内联元素。

**行内元素的特点：**

- 相邻行内元素在一行上，一行可以显示多个。
- 高、宽直接设置是无效的。
- 默认宽度就是它本身内容的宽度。
- 行内元素只能容纳文本或其他行内元素。

**注意：**
链接里面不能再放链接
特殊情况链接  里面可以放块级元素，但是给  转换一下块级模式最安全

#### 行内块元素

**常见的行内块标签**：

```md
<img />、<input />、<td>
```

它们同时具有块元素和行内元素的特点。有些资料称它们为行内块元素。

**行内块元素的特点**：

- 和相邻行内元素（行内块）在一行上，但是他们之间会有空白缝隙。
- 一行可以显示多个（行内元素特点）。
- 默认宽度就是它本身内容的宽度（行内元素特点）。
- 高度，行高、外边距以及内边距都可以控制（块级元素特点）。

#### 元素显示模式总结

学习元素显示模式的主要目的就是分清它们各自的特点，当我们网页布局的时候，在合适的地方用合适的标签元素。

### 元素显示模式的转换

**简单理解**:

一个模式的元素需要另外一种模式的特性
比如想要增加链接  的触发范围。

**转换方式**：

- 转换为块元素：display:block;
- 转换为行内元素：display:inline;
- 转换为行内块：display: inline-block;

### 单行文字垂直居中的代码

**解决方案**:

让文字的行高等于盒子的高度  就可以让文字在当前盒子内垂直居中

**简单理解**:

- 行高的上空隙和下空隙把文字挤到中间了，

- 如果行高小于盒子高度,文字会偏上，

- 如果行高大于盒子高度,则文字偏下。

---

## CSS 三大特性

### 层叠性

相同选择器给设置相同的样式，此时一个样式就会覆盖（层叠）另一个冲突的样式。层叠性主要解决样式冲突的问题

层叠性原则:

- 样式冲突，遵循的原则是就近原则，哪个样式离结构近，就执行哪个样式
- 样式不冲突，不会层叠

### 继承性

CSS中的继承: 子标签会继承父标签的某些样式，如文本颜色和字号。恰当地使用继承可以简化代码，降低 CSS 样式的复杂性。

子元素可以继承父元素的样式：

（text-，font-，line-这些元素开头的可以继承，以及color属性）

继承性口诀：龙生龙，凤生凤，老鼠生的孩子会打洞

行高的继承性：

```css
 body {
   font:12px/1.5 Microsoft YaHei；
 }
```

- 行高可以跟单位也可以不跟单位
- 如果子元素没有设置行高，则会继承父元素的行高为 1.5
- 此时子元素的行高是：当前子元素的文字大小 * 1.5
- body 行高 1.5  这样写法最大的优势就是里面子元素可以根据自己文字大小自动调整行高

### 优先级

当同一个元素指定多个选择器，就会有优先级的产生。

- 选择器相同，则执行层叠性
- 选择器不同，则根据选择器权重执行

选择器优先级计算表格：

优先级注意点:

1. 权重是有4组数字组成,但是不会有进位。
2. 可以理解为类选择器永远大于元素选择器, id选择器永远大于类选择器,以此类推..
3. 等级判断从左向右，如果某一位数值相同，则判断下一位数值。
4. 可以简单记忆法:  通配符和继承权重为0, 标签选择器为1,类(伪类)选择器为 10, id选择器 100, 行内样式表为 1000, !important 无穷大.
5. 继承的权重是0， 如果该元素没有直接选中，不管父元素权重多高，子元素得到的权重都是 0。

权重叠加：如果是复合选择器，则会有权重叠加，需要计算权重。

- div ul  li   ------>      0,0,0,3
- .nav ul li   ------>      0,0,1,2
- a:hover      -----—>   0,0,1,1
- .nav a       ------>      0,0,1,1

## CSS Box Model(盒子模型)

### 网页布局的本质

网页布局的核心本质： 就是利用 CSS 摆盒子。

网页布局过程：

1. 先准备好相关的网页元素，网页元素基本都是盒子 Box 。
2. 利用 CSS 设置好盒子样式，然后摆放到相应位置。
3. 往盒子里面装内容

### 盒子模型（Box Model）组成

盒子模型：把 HTML 页面中的布局元素看作是一个矩形的盒子，也就是一个盛装内容的容器。

CSS 盒子模型本质上是一个盒子，封装周围的 HTML 元素，它包括：**边框**、**外边距**、**内边距**、和 **实际内容**
![1571492529986.png](https://cdn.nlark.com/yuque/0/2023/png/29514937/1673671677805-9be45e80-3a21-4482-9340-a4e562d3b153.png#averageHue=%23ddf8b0&clientId=u3ffc37ac-2eb6-4&from=drop&id=ud7902032&originHeight=797&originWidth=1310&originalType=binary&ratio=1&rotation=0&showTitle=false&size=200491&status=done&style=none&taskId=u1ee3862c-3209-45df-a4ac-91fca34c873&title=)

不同部分的说明：

- **Margin(外边距)** - 清除边框外的区域，外边距是透明的。
- **Border(边框)** - 围绕在内边距和内容外的边框。
- **Padding(内边距)** - 清除内容周围的区域，内边距是透明的。
- **Content(内容)** - 盒子的内容，显示文本和图像。

### 元素的宽度和高度

当您指定一个 CSS 元素的宽度和高度属性时，你只是设置内容区域的宽度和高度。要知道，完整大小的元素，你还必须添加**内边距**，**边框**和**外边距**。

元素的总宽度计算公式：
**总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距**
元素的总高度计算公式：
**总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距**

```css
/* 元素的总宽度为 450px */
div {
    width: 300px;
    border: 25px solid green;
    padding: 25px;
    margin: 25px;
}
```

300px (宽) + 50px (左 + 右填充) + 50px (左 + 右边框) + 50px (左 + 右边距) = 450px

---

## CSS Border(边框)

| 属性 | 描述 |
| --- | --- |
| border | 简写属性，用于把针对四个边的属性设置在一个声明。 |
| border-style | 用于设置元素所有边框的样式，或者单独地为各边设置边框样式。 |
| border-width | 简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。 |
| border-color | 简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。 |
| border-bottom | 简写属性，用于把下边框的所有属性设置到一个声明中。 |
| border-bottom-color | 设置元素的下边框的颜色。 |
| border-bottom-style | 设置元素的下边框的样式。 |
| border-bottom-width | 设置元素的下边框的宽度。 |
| border-left | 简写属性，用于把左边框的所有属性设置到一个声明中。 |
| border-left-color | 设置元素的左边框的颜色。 |
| border-left-style | 设置元素的左边框的样式。 |
| border-left-width | 设置元素的左边框的宽度。 |
| border-right | 简写属性，用于把右边框的所有属性设置到一个声明中。 |
| border-right-color | 设置元素的右边框的颜色。 |
| border-right-style | 设置元素的右边框的样式。 |
| border-right-width | 设置元素的右边框的宽度。 |
| border-top | 简写属性，用于把上边框的所有属性设置到一个声明中。 |
| border-top-color | 设置元素的上边框的颜色。 |
| border-top-style | 设置元素的上边框的样式。 |
| border-top-width | 设置元素的上边框的宽度。 |
| border-radius | 设置圆角的边框。 |

border 可以设置元素的边框。边框有三部分组成：边框宽度(粗细)、边框样式、边框颜色

```css
 border : border-width || border-style || border-color;
```

### 边框样式

**border-style**属性用来定义边框的样式：

- none：没有边框即忽略所有边框的宽度 (默认值)
- solid：边框为单实线 (最为常用的)
- dashed：边框为虚线
- dotted：边框为点线
- double：边框为双实线 (两个边框的宽度和 border-width 的值相同)
- groove：3D沟槽边框 (效果取决于边框的颜色值)
- ridge：3D脊边框 (效果取决于边框的颜色值)
- inset：3D嵌入边框 (效果取决于边框的颜色值)
- outset：3D突出边框 (效果取决于边框的颜色值)

### 边框宽度

border-width 属性用来为边框指定宽度：

- 指定长度值，比如 2px 或 0.1em(单位为 px, pt, cm, em 等)
- 使用 3 个关键字之一， thick 、medium（默认值） 和 thin

**注意：**CSS 没有定义 3 个关键字的具体宽度，所以一个用户可能把 thick 、medium 和 thin 分别设置为等于 5px、3px 和 2px，而另一个用户则分别设置为 3px、2px 和 1px。

**注意：**"border-width" 属性单独使用不起作用。要先使用 "border-style" 属性设置边框。

```css
p.one {
    border-style:solid;
    border-width:5px;
}
p.two {
    border-style:solid;
    border-width:medium;
}
```

### 边框颜色

border-color属性用于设置边框的颜色。可以设置的颜色：

- name - 指定颜色的名称，如 "red"
- RGB - 指定 RGB 值, 如 "rgb(255,0,0)"
- Hex - 指定16进制值, 如 "#ff0000"
- transparent

**注意：** border-color单独使用是不起作用的，必须得先使用border-style来设置边框样式

```css
p.one {
    border-style:solid;
    border-color:red;
}
p.two {
    border-style:solid;
    border-color:#98bf21;
}
```

### 边框-单独设置各边

在CSS中，可以指定不同的侧面不同的边框：

border-style属性可以有1-4个值：

- **border-style : dotted solid double dashed;（**上->右->下->左**）**
  - 上边框是 dotted
  - 右边框是 solid
  - 底边框是 double
  - 左边框是 dashed

- **border-style : dotted solid double;（**上->左右->下**）**
  - 上边框是 dotted
  - 左、右边框是 solid
  - 底边框是 double

- **border-style : dotted solid;（**上下->左右**）**
  - 上、底边框是 dotted
  - 右、左边框是 solid

- **border-style : dotted;（**上下左右属性相同**）**
  - 四面边框是 dotted

```css
p {
  border-top-style : dotted;
  border-right-style : solid;
  border-bottom-style : dotted;
  border-left-style : solid;
  /* border-style:dotted solid; */
}
```

### 边框简写

边框简写：

```css
 border: 1px solid red;
```

边框分开写法：

```css
 border-top: 1px solid red;  /* 只设定上边框， 其余同理 */
```

### 表格的细线边框

border-collapse 属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框。

```css
 border-collapse:collapse;
```

collapse 单词是合并的意思
border-collapse: collapse; 表示相邻边框合并在一起

### 边框会影响盒子实际大小

边框会额外增加盒子的实际大小。因此我们有两种方案解决：

- 测量盒子大小的时候,不量边框。
- 如果测量的时候包含了边框,则需要 width/height 减去边框宽度

---

## CSS Outline(轮廓)

| 属性 | 说明 | 值 | CSS |
| --- | --- | --- | --- |
| outline | 在一个声明中设置所有的轮廓属性 | _outline-color
outline-style
outline-width
_inherit | 2 |
| outline-color | 设置轮廓的颜色 | _color-name
hex-number
rgb-number
_invert
inherit | 2 |
| outline-style | 设置轮廓的样式 | none
dotted
dashed
solid
double
groove
ridge
inset
outset
inherit | 2 |
| outline-width | 设置轮廓的宽度 | thin
medium
thick
_length
_inherit | 2 |

轮廓（outline）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

outline 属性指定元素轮廓的样式、颜色和宽度。

![box_outline.gif](https://cdn.nlark.com/yuque/0/2023/gif/29514937/1673774456626-6a5994df-78fb-48ad-8bb4-56eb0c05b747.gif#averageHue=%23f4f4f4&clientId=u318a6347-5c9f-4&from=drop&height=264&id=u2e909450&originHeight=289&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3889&status=done&style=none&taskId=u3068d868-a582-48cc-8ae1-dd7dddca28f&title=&width=489)
>
> 1. outline是不占空间的，既不会增加额外的width或者height（这样不会导致浏览器渲染时出现reflow或是repaint）
> 2. outline有可能是非矩形的（火狐浏览器下）

---

## CSS Padding(内边距/填充)

### 内边距的使用方式

1、padding 属性用于设置内边距，即边框与内容之间的距离。

2、语法：

合写属性：
分写属性：

### 内边距会影响盒子实际大小

1、当我们给盒子指定 padding 值之后，发生了 2 件事情：

1. 内容和边框有了距离，添加了内边距。
2. padding影响了盒子实际大小。

2、内边距对盒子大小的影响：

- 如果盒子已经有了宽度和高度，此时再指定内边框，会撑大盒子。
- 如何盒子本身没有指定width/height属性, 则此时padding不会撑开盒子大小。

3、解决方案：

如果保证盒子跟效果图大小保持一致，则让 width/height 减去多出来的内边距大小即可。

## CSS Margin(外边距)

| 属性 | 描述 |
| --- | --- |
| margin | 简写属性。在一个声明中设置所有外边距属性。 |
| margin-bottom | 设置元素的下外边距。 |
| margin-left | 设置元素的左外边距。 |
| margin-right | 设置元素的右外边距。 |
| margin-top | 设置元素的上外边距。 |

margin 属性定义元素周围的空间（用于设置外边距），即控制盒子和盒子之间的距离：

1. margin 清除周围的（外边框）元素区域。margin 没有背景颜色，是完全透明的。
2. margin 可以单独改变元素的上，下，左，右边距，也可以一次改变所有的属性。

![VlwVi.png](https://cdn.nlark.com/yuque/0/2023/png/29514937/1673774772050-63b694bc-aa4c-4d28-a167-c3c92305d2cd.png#averageHue=%23030000&clientId=u318a6347-5c9f-4&from=drop&height=240&id=u29caee46&originHeight=300&originWidth=600&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7406&status=done&style=none&taskId=u980b5307-0190-4f43-acaa-fd65fca042d&title=&width=480)

### 可能的值

| 值 | 说明 |
| --- | --- |
| auto | 设置浏览器边距。
这样做的结果会依赖于浏览器 |
| *length* | 定义一个固定的margin（使用像素，pt，em等） |
| *%* | 定义一个使用百分比的边距 |

> Margin可以使用负值，重叠的内容。

### 单边外边距

在CSS中，它可以指定不同的侧面不同的边距：

```css
margin-top : 100px;
margin-bottom : 100px;
margin-right : 50px;
margin-left : 50px;
```

### 外边距简写

所有边距属性的简写属性是 **margin** :

```css
margin : 100px 50px;
```

margin属性可以有一到四个值。

- **margin : 25px 50px 75px 100px;**

  - 上边距为25px
  - 右边距为50px
  - 下边距为75px
  - 左边距为100px
- **margin : 25px 50px 75px;**

  - 上边距为25px
  - 左右边距为50px
  - 下边距为75px
- **margin : 25px 50px;**

  - 上下边距为25px
  - 左右边距为50px
- **margin : 25px;**
  - 所有的4个边距都是25px

### 外边距典型应用

外边距可以让块级盒子水平居中的两个条件：

- 盒子必须指定了宽度（width）。
- 盒子左右的外边距都设置为 auto 。

常见的写法，以下三种都可以：

```css
margin-left: auto;   margin-right: auto;
margin: auto;
margin: 0 auto;
```

**注意：**以上方法是让块级元素水平居中，行内元素或者行内块元素水平居中给其父元素添加 text-align : center 即可。

### 外边距合并

使用 margin 定义块元素的垂直外边距时，可能会出现外边距的合并。

主要有两种情况：

1. 相邻块元素垂直外边距的合并

当上下相邻的两个块元素（兄弟关系）相遇时，如果上面的元素有下外边距 margin-bottom，下面的元素有上外边距 margin-top ，则他们之间的垂直间距不是 margin-bottom 与 margin-top 之和。取两个值中的较大者这种现象被称为相邻块元素垂直外边距的合并。

解决方案：尽量只给一个盒子添加 margin 值。

2. 嵌套块元素垂直外边距的塌陷

对于两个嵌套关系（父子关系）的块元素，父元素有上外边距同时子元素也有上外边距，此时父元素会塌陷较大的外边距值。

解决方案：

- 可以为父元素定义上边框。
- 可以为父元素定义上内边距。
- 可以为父元素添加 overflow:hidden。

### 清除内外边距

网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。因此我们在布局前，首先要清除下网页元素的内外边距。

```css
 * {
    padding:0;   /* 清除内边距 */
    margin:0;    /* 清除外边距 */
  }
```

注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素就可以了

---

## 其他样式

### 圆角边框

在 CSS3 中，新增了圆角边框样式，这样我们的盒子就可以变圆角了。

border-radius 属性用于设置元素的外边框圆角。

```css
 border-radius:length;
```

- 参数值可以为数值或百分比的形式
- 如果是正方形，想要设置为一个圆，把数值修改为高度或者宽度的一半即可，或者直接写为 50%
- 该属性是一个简写属性，可以跟四个值，分别代表左上角、右上角、右下角、左下角
- 分开写：border-top-left-radius、border-top-right-radius、border-bottom-right-radius 和border-bottom-left-radius
- 兼容性 ie9+ 浏览器支持, 但是不会影响页面布局,可以放心使用

### 盒子阴影

CSS3 中新增了盒子阴影，我们可以使用 box-shadow 属性为盒子添加阴影。
语法：

```css
 box-shadow: h-shadow v-shadow blur spread color inset;
```

### 文字阴影

在 CSS3 中，我们可以使用 text-shadow 属性将阴影应用于文本。

```css
 text-shadow: h-shadow v-shadow blur color;
```

---

## CSS Float(浮动)

### 传统网页布局的三种方式

CSS 提供了三种传统布局方式(简单说,就是盒子如何进行排列顺序)：

- 普通流（标准流）
- 浮动
- 定位
这三种布局方式都是用来摆放盒子的，盒子摆放到合适位置，布局自然就完成了。

注意：实际开发中，一个页面基本都包含了这三种布局方式（后面移动端学习新的布局方式） 。

### 标准流（普通流/文档流）

所谓的标准流:  就是标签按照规定好默认方式排列

1. 块级元素会独占一行，从上向下顺序排列。常用元素：div、hr、p、h1~h6、ul、ol、dl、form、table
2. 行内元素会按照顺序，从左到右顺序排列，碰到父元素边缘则自动换行。常用元素：span、a、i、em 等

以上都是标准流布局，我们前面学习的就是标准流，标准流是最基本的布局方式。

### 为什么需要浮动？

总结： 有很多的布局效果，标准流没有办法完成，此时就可以利用浮动完成布局。 因为浮动可以改变元素标签默认的排列方式.

浮动最典型的应用：可以让多个块级元素一行内排列显示。

网页布局第一准则：**多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动**。

### 什么是浮动？

float 属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘。

```css
 选择器 { float: 属性值; }
```

### 浮动特性

加了浮动之后的元素,会具有很多特性,需要我们掌握的.

1、浮动元素会脱离标准流(脱标：浮动的盒子不再保留原先的位置)

<!-- ![](images%5C1571544664994.png#id=uBHuN&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) -->

2、浮动的元素会一行内显示并且元素顶部对齐

<!-- ![](images%5C1571544725757.png#id=BrC4D&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) -->

注意：

浮动的元素是互相贴靠在一起的（不会有缝隙），如果父级宽度装不下这些浮动的盒子，多出的盒子会另起一行对齐。

3、浮动的元素会具有行内块元素的特性

浮动元素的大小根据内容来决定

浮动的盒子中间是没有缝隙的

### 浮动元素和标准流父级

浮动元素经常和标准流父级搭配使用

为了约束浮动元素位置, 我们网页布局一般采取的策略是:

先用标准流父元素排列上下位置, 之后内部子元素采取浮动排列左右位置.  符合网页布局第一准侧

<!-- ![](images%5C1571544991989.png#id=Hp550&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=) -->

### 常见网页布局

#### 浮动布局注意点

1、浮动和标准流的父盒子搭配。

先用标准流的父元素排列上下位置, 之后内部子元素采取浮动排列左右位置

2、一个元素浮动了，理论上其余的兄弟元素也要浮动。

一个盒子里面有多个子盒子，如果其中一个盒子浮动了，其他兄弟也应该浮动，以防止引起问题。

浮动的盒子只会影响浮动盒子后面的标准流,不会影响前面的标准流.

### 清除浮动

#### 为什么需要清除浮动？

由于父级盒子很多情况下，不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为 0 时，就会影响下面的标准流盒子。

#### 清除浮动本质

清除浮动的本质是清除浮动元素造成的影响：浮动的子标签无法撑开父盒子的高度

注意：

- 如果父盒子本身有高度，则不需要清除浮动
- 清除浮动之后，父级就会根据浮动的子盒子自动检测高度。
- 父级有了高度，就不会影响下面的标准流了

#### 清除浮动样式

clear 属性指定元素两侧不能出现浮动元素。使用 clear 属性往文本中添加图片廊：
清除浮动的策略是:  闭合浮动

```css
/* 选择器{clear:属性值;} */
.text_line {
    clear:both;
}
```

#### 清除浮动的多种方式

#### 额外标签法

额外标签法也称为隔墙法，是 W3C 推荐的做法。

使用方式：额外标签法会在浮动元素末尾添加一个空的标签。

```html
例如 <div style="clear:both"></div>，或者其他标签（如
等）。
```

优点： 通俗易懂，书写方便

缺点： 添加许多无意义的标签，结构化较差

注意： 要求这个新的空标签必须是块级元素。

1、清除浮动本质是：清除浮动的本质是清除浮动元素脱离标准流造成的影响

2、清除浮动策略是：闭合浮动.  只让浮动在父盒子内部影响,不影响父盒子外面的其他盒子.

3、额外标签法：隔墙法, 就是在最后一个浮动的子元素后面添

4、加一个额外标签, 添加 清除浮动样式.实际工作可能会遇到,但是不常用

#### 父级添加 overflow 属性

可以给父级添加 overflow 属性，将其属性值设置为 hidden、 auto 或 scroll

```css
overflow:hidden | auto | scroll;
```

优点：代码简洁

缺点：无法显示溢出的部分

注意：是给父元素添加代码

#### 父级添加after伪元素

:after 方式是额外标签法的升级版。给父元素添加：

```css
 .clearfix:after {  
   content: ""; 
   display: block; 
   height: 0; 
   clear: both; 
   visibility: hidden;  
 } 
 .clearfix {  /* IE6、7 专有 */ 
   *zoom: 1;
 }
```

优点：没有增加标签，结构更简单

缺点：照顾低版本浏览器

代表网站： 百度、淘宝网、网易等

#### 父级添加双伪元素

给父元素添加

```css
 .clearfix:before,.clearfix:after {
   content:"";
   display:table; 
 }
 .clearfix:after {
   clear:both;
 }
 .clearfix {
    *zoom:1;
 }
```

优点：代码更简洁

缺点：照顾低版本浏览器

代表网站：小米、腾讯等

为什么需要清除浮动？

1. 父级没高度
2. 子盒子浮动了
3. 影响下面布局了，我们就应该清除浮动了
