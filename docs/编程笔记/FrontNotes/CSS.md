# CSS

## 1 概念
+ 概念：CSS(Cascading Style Sheets)  ，通常称为CSS样式表或**层叠样式表**（级联样式表）。
+ 作用：
    - 主要用于**设置** HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及**版面的布局和外观显示样式。**
    - CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。

## 2 引入CSS样式表的方式
### 1 行内式（内联样式）
是通过标签的style属性来设置元素的样式

```css
<div style="color: red; font-size: 12px;">青春不常在，抓紧谈恋爱</div>
```



### 2 内部样式表
是将CSS代码集中写在HTML文档头部标签中，并且用style标签定义。

```css
<style>
	 div {
	 	color: red;
	 	font-size: 12px;
	 }
</style>
```

+ 注意：
    - style标签一般位于head标签中，当然理论上他可以放在HTML文档的任何地方。
    - type="text/css"  在html5中可以**省略**。



### 3 外部样式表
+ 是将所有的样式放在一个或多个以**.CSS**为扩展名的外部样式表文件中，
+ 通过link标签将外部样式表文件链接到HTML文档中

```html
<head>
  <link rel="stylesheet" type="text/css" href="css文件路径">
</head>
```

+ 注意：
    - link 是个单标签
    - link标签需要放在head头部标签中，并且指定link标签的三个属性



| 属性 | 作用 |
| --- | --- |
| rel | 定义当前文档与被链接文档之间的关系，在这里需要指定为“**stylesheet**”，表示被链接的文档是一个样式表文件。 |
| type | 定义所链接文档的类型，在这里需要指定为“**text/CSS**”，表示链接的外部文件为CSS样式表。我们都可以**省略** |
| href | 定义所链接外部样式表文件的URL，可以是相对路径，也可以是绝对路径。 |




---

# 二、层叠与继承
## 1 层叠性
<font style="color:#333333;">Stylesheets </font>**cascade（样式表层叠）**<font style="color:#333333;"> </font>

有三个因素需要考虑，根据重要性排序如下，前面的更重要：

### 1. 重要性
在CSS中，属性值后面加上 !important 可以让这条规则优先于其他规则。



### 2. 优先级
> **优先级:!important语法 >行内式> ID选择器 > 类选择器 > 元素选择器**
>

> !important > 内联样式 > ID 选择器 > 类选择器 = 属性选择器 = 伪类选择器 > 标签选择器 = 伪元素选择器 > 通配符选择器 > 继承 > 浏览器默认属性
>

一个选择器的优先级可以说是由四个部分相加 (分量)，可以认为是个四位数的四个位数：

1. **千位**： 如果声明在 `[style](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes#attr-style)` 的属性（内联样式）则该位得一分。这样的声明没有选择器，所以它得分总是1000。
2. **百位**： 选择器中包含ID选择器则该位得一分。
3. **十位**： 选择器中包含类选择器、属性选择器或者伪类则该位得一分。
4. **个位**：选择器中包含元素、伪元素选择器则该位得一分。

**注**: 通用选择器 (`*`)，组合符 (`+`, `>`, `~`, ' ')，和否定伪类 (`:not`) 不会影响优先级。

**警告: **在进行计算时不允许进行进位，例如，20 个类选择器仅仅意味着 20 个十位，而不能视为 两个百位，也就是说，无论多少个类选择器的权重叠加，都不会超过一个 ID 选择器。

| 选择器 | 千位 | 百位 | 十位 | 个位 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| `h1` | 0 | 0 | 0 | 1 | 0001 |
| `h1 + p::first-letter` | 0 | 0 | 0 | 3 | 0003 |
| `li > a[href*="en-US"] > .inline-warning` | 0 | 0 | 2 | 2 | 0022 |
| `#identifier` | 0 | 1 | 0 | 0 | 0100 |
| 内联样式 | 1 | 0 | 0 | 0 | 1000 |




### 3. 资源顺序
<font style="color:#333333;">简单的说，css规则的顺序很重要；当应用两条同级别的规则到一个元素的时候，写在后面的就是实际使用的规则。</font>



## 2 继承性
+ 关于文字样式的，都能够继承； 所有关于盒子的、定位的、布局的属性都不能继承。
+ <font style="color:#333333;">哪些属性属于默认继承很大程度上是由常识决定的。</font>



**默认继承的 ("Inherited: Yes") 的属性：****<font style="color:#F5222D;">（大多是和文本相关的）</font>**

+ 所有元素默认继承：visibility、cursor
+ 文本属性默认继承：letter-spacing、word-spacing、white-space、line-height、color、font、 font-family、font-size、font-style、font-variant、font-weight、text-indent、text-align、text-shadow、text-transform、direction
+ 列表元素默认继承：list-style、list-style-type、list-style-position、list-style-image
+ 表格元素默认继承：border-collapse

****

**默认不继承的("Inherited: No") 的属性：**

+ 所有元素默认不继承：all、display、overflow、contain
+ 文本属性默认不继承：vertical-align、text-decoration、text-overflow
+ 盒子属性默认不继承：width、height、padding、margin、border、min-width、min-height、max-width、max-height
+ 背景属性默认不继承：background、background-color、background-image、background-repeat、background-position、background-attachment
+ 定位属性默认不继承：float、clear、position、top、right、bottom、left、z-index
+ 内容属性默认不继承：content、counter-reset、counter-increment
+ 轮廓属性默认不继承：outline-style、outline-width、outline-color、outline
+ 页面属性默认不继承：size、page-break-before、page-break-after
+ 声音属性默认不继承：pause-before、pause-after、pause、cue-before、cue-after、cue、play-during



### 控制继承
+ `[inherit](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inherit)`设置该属性会使子元素属性和父元素相同。实际上，就是 "开启继承".
+ `[initial](https://developer.mozilla.org/zh-CN/docs/Web/CSS/initial)`设置属性值和浏览器默认样式相同。如果浏览器默认样式中未设置且该属性是自然继承的，那么会设置为 `inherit` 。
+ `[unset](https://developer.mozilla.org/zh-CN/docs/Web/CSS/unset)`将属性重置为自然值，也就是如果属性是自然继承那么就是 `inherit`，否则和 `initial`一样



注：initial 和 unset 不被IE支持， 还有一个新的属性, `[revert](https://developer.mozilla.org/zh-CN/docs/Web/CSS/revert)`， 只有很少的浏览器支持。





---



# 三、显示模式（display）
标签以什么方式进行显示，比如div 自己占一行， 比如span 一行可以放很多个。HTML标签一般分为块标签和行内标签两种类型，它们也称块元素和行内元素。

## 1 块级元素(block-level)
每个块元素通常都会独自占据一整行或多整行，可以对其设置宽度、高度、对齐等属性，常用于网页布局和网页结构的搭建。常见的块元素有<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中<div>标签是最典型的块元素。

**块级元素的特点：**

+ 比较霸道，自己独占一行
+ 高度，宽度、外边距以及内边距都可以控制。
+ **<font style="color:#F5222D;">宽度默认是容器（父级宽度）的100%</font>**
+ 是一个容器及盒子，里面可以放行内或者块级元素。
+ 同理还有这些标签h1,h2,h3,h4,h5,h6,dt，他们都是文字类块级标签，里面不能放其他块级元素。

## 2 行内元素(inline-level)
常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。有的地方称为内联元素

**行内元素的特点：**

+ 相邻行内元素在一行上，一行可以显示多个。
+ **<font style="color:#F5222D;">高、宽直接设置是无效的</font>**<font style="color:#F5222D;">。</font>
+ **<font style="color:#F5222D;">默认宽度就是它本身内容的宽度</font>**<font style="color:#F5222D;">。</font>
+ 行内元素只能容纳文本或则其他行内元素。



## 3 行内块元素（inline-block）
在行内元素中有几个特殊的标签——<img />、<input />、<td>，可以对它们设置宽高和对齐属性，有些资料可能会称它们为行内块元素。

**行内块元素的特点：**

+ 和相邻行内元素（行内块）在一行上,但是之间会有空白缝隙。一行可以显示多个
+ 默认宽度就是它本身内容的宽度。
+ 高度，行高、外边距以及内边距都可以控制。



**<font style="color:#F5222D;">行内块之间会有间隙：</font>**间隙来自于标签之间的空白

解决方法：

+ <font style="color:rgb(77, 77, 77);">标签之间不换行（不优雅）</font>
+ <font style="color:rgb(77, 77, 77);">给父元素设置font-size:0 ，</font>**<font style="color:rgb(77, 77, 77);">子元素别忘了设置font-size</font>**





## 4 总结
| 元素模式 | 元素排列 | 设置样式 | 默认宽度 | 包含 |
| --- | --- | --- | --- | --- |
| 块级元素 | 一行只能放一个块级元素 | 可以设置宽度高度 | 容器的100% | 容器级可以包含任何标签 |
| 行内元素 | 一行可以放多个行内元素 | 不可以直接设置宽度高度 | 它本身内容的宽度 | 容纳文本或则其他行内元素 |
| 行内块元素 | 一行放多个行内块元素 | 可以设置宽度和高度 | 它本身内容的宽度 |  |


# 四、元素的显示与隐藏
+ <font style="color:rgb(51, 51, 51);">目的（本质）	让一个元素在页面中消失或者显示出来</font>

### <font style="color:rgb(51, 51, 51);">7.1. display 显示（重点）</font>
+ <font style="color:rgb(51, 51, 51);">display 设置或检索对象是否及如何显示。</font>
+ `<font style="color:rgb(51, 51, 51);">display: none</font>`<font style="color:rgb(51, 51, 51);"> 隐藏对象</font>
+ `<font style="color:rgb(51, 51, 51);">display：block</font>`<font style="color:rgb(51, 51, 51);">  除了转换为块级元素之外，同时还有显示元素的意思。</font>
+ <font style="color:rgb(51, 51, 51);">特点： display 隐藏元素后，</font>**<font style="color:rgb(51, 51, 51);">不再占</font>**<font style="color:rgb(51, 51, 51);">有原来的位置。</font>



### <font style="color:rgb(51, 51, 51);">7.2. visibility 可见性 （了解）</font>
+ <font style="color:rgb(51, 51, 51);">visibility 属性用于指定一个元素应可见还是隐藏。</font>
+ `<font style="color:rgb(51, 51, 51);">visibility：visible</font>`<font style="color:rgb(51, 51, 51);">　元素可视</font>
+ `<font style="color:rgb(51, 51, 51);">visibility：hidden</font>`<font style="color:rgb(51, 51, 51);">　  元素隐藏</font>
+ <font style="color:rgb(51, 51, 51);">特点：</font>**<font style="color:rgb(51, 51, 51);">visibility 隐藏元素后，继续占有原来的位置</font>**<font style="color:rgb(51, 51, 51);">。</font>



+ <font style="color:rgb(51, 51, 51);">如果隐藏元素想要原来位置， 就用 visibility：hidden</font>
+ <font style="color:rgb(51, 51, 51);">如果隐藏元素不想要原来位置， 就用 display：none (用处更多 重点）</font>

### <font style="color:rgb(51, 51, 51);">7.3. overflow 溢出（重点）</font>
+ <font style="color:rgb(51, 51, 51);">overflow 属性指定了如果内容溢出一个元素的框（超过其指定高度及宽度） 时，会发生什么。</font>

| **<font style="color:rgb(51, 51, 51);">属性值</font>** | **<font style="color:rgb(51, 51, 51);">描述</font>** |
| :--- | :--- |
| **<font style="color:rgb(51, 51, 51);">visible</font>** | <font style="color:rgb(51, 51, 51);">不剪切内容也不添加滚动条</font> |
| **<font style="color:rgb(51, 51, 51);">hidden</font>** | <font style="color:rgb(51, 51, 51);">不显示超过对象尺寸的内容，超出的部分隐藏掉</font> |
| **<font style="color:rgb(51, 51, 51);">scroll</font>** | <font style="color:rgb(51, 51, 51);">不管超出内容否，总是显示滚动条</font> |
| **<font style="color:rgb(51, 51, 51);">auto</font>** | <font style="color:rgb(51, 51, 51);">超出自动显示滚动条，不超出不显示滚动条</font> |


+ <font style="color:rgb(51, 51, 51);">一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局。</font>
+ <font style="color:rgb(51, 51, 51);">但是如果有定位的盒子， 请慎用overflow:hidden 因为它会隐藏多余的部分。</font>
+ <font style="color:rgb(51, 51, 51);">实际开发场景：</font>
    1. <font style="color:rgb(51, 51, 51);">清除浮动</font>
    2. <font style="color:rgb(51, 51, 51);">隐藏超出内容，隐藏掉, 不允许内容超过父盒子。</font>

### <font style="color:rgb(51, 51, 51);">7.4. 显示与隐藏总结</font>
| **<font style="color:rgb(51, 51, 51);">属性</font>** | **<font style="color:rgb(51, 51, 51);">区别</font>** | **<font style="color:rgb(51, 51, 51);">用途</font>** |
| :--- | :--- | :--- |
| **<font style="color:rgb(51, 51, 51);">display 显示 （重点）</font>** | <font style="color:rgb(51, 51, 51);">隐藏对象，不保留位置</font> | <font style="color:rgb(51, 51, 51);">配合后面js做特效，比如下拉菜单，原先没有，鼠标经过，显示下拉菜单， 应用极为广泛</font> |
| **<font style="color:rgb(51, 51, 51);">visibility 可见性 （了解）</font>** | <font style="color:rgb(51, 51, 51);">隐藏对象，保留位置</font> | <font style="color:rgb(51, 51, 51);">使用较少</font> |
| **<font style="color:rgb(51, 51, 51);">overflow 溢出（重点）</font>** | <font style="color:rgb(51, 51, 51);">只是隐藏超出大小的部分</font> | <font style="color:rgb(51, 51, 51);">1. 可以清除浮动 2. 保证盒子里面的内容不会超出该盒子范围</font> |






> 更新: 2024-02-18 17:26:21  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/rux51l1wspfiugxk>