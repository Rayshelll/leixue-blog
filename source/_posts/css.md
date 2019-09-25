---
title: css
date: 2019-08-19 16:10:39
tags: 
- CSS
---
### CSS行内元素在块状元素中水平垂直居中
1. 块状元素：
    - `display:block;`
    - 标签：div、p、ul-li、address、h1-h6、blockquote、dl、dt、dd、nav、aside、header、footer、section、article；
    - 特性：
        1. 能够识别宽高；
        2. margin和padding的上下左右均对其有效；
        3. 可以自动换行；
        4. 多个块状元素标签写在一起，默认排列方式为从上至下；
    - 水平居中实现方式：
        1. 子元素`{margin:0 auto;}`
        2. 子元素`{position: relative/absolute; left: 50%;}`
        3. 父元素`display: flex; justify-content: center`
    - 垂直居中实现方式：    
        1. 父元素：`display: flex; align-items: center;`
        2. 父元素：`position: relative;` 子元素：`position: absolute; top: 50%; margin-top: -height（子）/2;`
        3. 父元素：`position: relative;` 子元素：`position:absolute; top:0; bottom:0;margin:auto;`
    - 水平垂直居中实现方式：
        1. 父元素：`display: flex;justify-content: center;align-items: center;`
        2. 父元素：`display:flex; `子元素：`margin:auto;`
        3. 父元素：`position: relative;` 子元素：`position: absolute; top: 50%; left: 50%; margin-top: -height（子）/2; margin-right: -width/2;(已知块级元素的宽和高)`
        4. 父元素：`position:relative` 子元素：`position: absolute; top:0; left:0; bottom:0; right:0; margin:auto;` 

<!-- more -->

2. 行内元素：
    - `display:inline;`
    - a、b、span、img、input、strong、select、label、em、button、textarea（字体、input类、span）等；
    - 特性：
        1. 设置宽高无效；
        2. 对margin仅设置左右方向有效，上下无效；padding设置上下左右都有效，即会撑大空间；
        3. 不会自动进行换行；
    - 水平居中实现方式：
        1. 父元素`text-align:center`
    - 垂直居中实现方式：
        1. 子元素`line-height:height(父);`
        2. 父元素`display: table-cell; vertical-align:middle;`   
    - 水平垂直居中实现方式：           
        1. 父元素`display: table-cell; vertical-align: middle; text-align: center;`  
        2. 父元素`text-align:center` 子元素`line-height:height(父);`

3. 行内块状元素：
    - `display:inline-block;`
    - 特征：
        1. 不自动换行
        2. 能够识别宽高
        3. 默认排列方式为从左到右；(行内元素和块状元素都使用)

### css相对定位、绝对定位
1. 绝对定位(`position:absolute`)生成绝对定位的元素（脱离文档流），相对于 `static` 定位以外的第一个父元素进行定位(如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口)。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
2. 相对定位(`position:relative`)生成相对定位的元素(没有脱离文档流)，相对于自身正常位置进行定位。移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动.
3. 固定定位(`position: fixed`) 与`background-attachment:fixed;`属性功能相同。生成绝对定位的元素(脱离文档流)，相对于浏览器窗口进行定位。不受窗口大小变化和滚动条而改变位置
4. `position:static`默认值，没有定位，元素出现在正常的流中；`position:inherit`规定应该从父元素继承 position 属性的值。
5. 嵌套使用：子容器在父容器底部居中：父容器：`position：relative；`子容器：`position：absolute；bottom：0；left：0；right：0；margin: auto`

### CSS hack
CSS hack是通过在CSS样式中加入一些特殊的符号，让不同的浏览器识别不同的符号，以达到应用不同的CSS样式的目的。(不同浏览器识别不同css样式)
比如IE6能识别下划线“_”和星号“*”，IE7能识别星号“*”，但不能识别下划线”_ ”，而firefox两个都不能认识。
``` css
div {
    background:green;*background:red;
}
```
#### 浏览器的内核分别是什么?经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧？
- 浏览器的内核
    1. IE浏览器的内核Trident、
    2. Mozilla的Gecko、google的WebKit、
    3. Opera内核Presto；
- 浏览器的兼容性：
    1. png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8位.
    2. 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

### CSS 选择器
- CSS 选择器
    1. id选择器(# myid)
    2. 类选择器(.myclassname)
    3. 标签选择器(div, h1, p)
    4. 相邻选择器(h1 + p)
    5. 子选择器(ul > li)
    6. 后代选择器(li a)
    7. 通配符选择器( * )
    8. 属性选择器(a[rel = "external"])
    9. 伪类选择器(a: hover, li:nth-child)
- 可继承的样式：1.font-size 2.font-family 3.color 4.text-indent
- 不可继承的样式：1.border 2.padding 3.margin 4.width 5.height
- 优先级算法：
    1. 优先级就近原则，同权重情况下样式定义最近者为准;
    2. 载入样式以最后载入的定位为准;
    3. !important > 内联> id > class > tag  
- CSS伪类：
    `p:first-of-type` 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    `p:last-of-type ` 选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    `p:only-of-type ` 选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    `p:only-child `   选择属于其父元素的唯一子元素的每个 <p> 元素。
    `p:nth-child(2) ` 选择属于其父元素的第二个子元素的每个 <p> 元素。
    :first-child 与 :first-of-type的不同
    `:first-child` 匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素。
    `:first-of-type` 匹配的是该类型的第一个
    `:enabled `/ `:disabled` 控制表单控件的禁用状态。
    `:checked`  单选框或复选框被选中。
    `:before` / `:after` 定义对象之前/之后内容的样式
    `:first-letter` / `:first-line` 定义文本的第一个字符/首行样式 只能用于块级元素
    `:hover` / `:link` / `:focus` / `:visited` / `:active`
    

### 盒模型
- 标准W3C盒子模型：
    1. width = content；
    2. box-sizing: content-box；(默认)
    3. 渲染wh受 padding border 等属性影响，动态大小

- IE盒子模型中：
    1. width = content + padding + border；
    2. box-sizing: border-box；
    3. 渲染wh不受 padding border 等属性影响，固定大小

### Flex布局
**传统布局**基于盒状模型，依赖 `display`属性 + `position`属性 + `float`属性( 缺点：垂直居中等不好实现) 
**Flex**是Flexible Box的缩写，意为”弹性布局”
有两个重要概念：**容器**和**项目**(容器的子成员)
***注意***，设为Flex布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。

语法：
``` css
.box {
    display: flex;
    display: flex-inline; /* 行内元素flex布局 */
    display: -webkit-flex; /* 
    Webkit内核的浏览器Safari */
}
```

#### 容器的属性
6个属性：
`flex-direction`  项目的排列**方向**
`flex-wrap` 项目排列是否**换行**
`flex-flow` 前两项的简写
`justify-content` 项目在**主轴**上的**对齐方式**
`align-items` 项目在**竖轴**上如何**对齐方式**
`align-content` **多根轴线**的**对齐方式**，只有一根轴线，该属性不起作用

``` css
.box {
    flex-direction: row(从左到右) / row-reverse (从右到左) / column (从上到下) / column-reverse(从下到上);
    flex-wrap: nowrap(默认值不换行)  / wrap(换行，第一行在上方)  / wrap-reverse(换行，第一行在下方) ;
    flex-flow: <flex-direction> <flex-wrap>;
    justify-content: flex-start(左对齐) / flex-end(右对齐)  / center (居中) / space-between(两端对齐)  / space-around(间隔相等);
    align-items: stretch(默认值，未设高度拉伸填满) / flex-start(起点对齐)  / flex-end (终点对齐) / center (中点对齐) / baseline(第一行文字的基线对齐);
    align-content: flex-start / flex-end / center / space-between / space-around / stretch;
}
```

#### 项目的属性
6个属性：
`order` 项目的排列顺序。数值越小，排列越靠前，默认为0
`flex-grow` 项目的放大比例，默认为0
`flex-shrink` 项目的缩小比例，默认为1
`flex-basis` 项目占据的主轴空间
`flex` **前三个的简写，优先使用这个属性**
`align-self` 允许单个项目有与其他项目不一样的对齐方式,可覆盖容器属性align-items属性

``` css
.item {
    order: <integer>;
    flex-grow: <number>; /* default 0 */
    flex-shrink: <number>; /* default 1 负值对该属性无效*/
    flex-basis: <length> / auto; /* default auto */
    flex: none(0 0 auto) / auto(1 1 auto)/*默认值为0 1 auto*/
    align-self: auto / flex-start / flex-end / center / baseline / stretch; /*默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。*/
}
/* flex的不同取值 */
.item {flex: 2333 3222 234px;}
.item {
    flex-grow: 2333;
    flex-shrink: 3222;
    flex-basis: 234px;
}
.item {flex: 1;}/*非负整数*/
.item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0%;
}
.item-1 {flex: 0%;}/*百分比*/
.item-1 {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0%;
}
.item-2 {flex: 24px;}/*像素值*/
.item-1 {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 24px;
}
.item {flex: 2 3;}/*两个非负整数*/
.item {
    flex-grow: 2;
    flex-shrink: 3;
    flex-basis: 0%;
}
.item {flex: 2333 3222px;}/*一个非负整数 一个像素值*/
.item {
    flex-grow: 2333;
    flex-shrink: 1;
    flex-basis: 3222px;
}
```
#### flex布局的应用：css两栏，一栏固定宽度，一栏自适应
第一个div固定，第二个div自适应
``` css
/*使用flex布局实现*/
/*父*/
.container{
  display:flex;
  height:100px;
}
/*子*/
.box1{
  flex: 0 0 200px;
  background:blue;
}
.box2{
  flex: 1;/*flex:auto*/
  background:red;
}
/*利用 float 配合 margin或overflow: hidden; 实现*/
.container{
  height:100px;
}
.box1{
  width:200px;
  float:left;
  background: blue;
  height: 100%;
}
.box2{
  margin-left: 100px;/* overflow: hidden;*/
  background: red;
  height: 100%;
}
```
#### flex布局的应用：在一个大盒子里面有两个小盒子，两个小盒子都水平居中，其中一个贴紧上边，另一个贴紧下边。要求：不可以给两个小盒子加样式，只能给大盒子写样式。
``` css
.container{
  display:flex;
  flex-direction:column;
  height:400px;
  justify-content:space-between;
  align-items:center;
}
.box1{
  width:200px;
  background: blue;
  height: 50px;
}
.box2{
  background: red;
  height: 50px;
  width:200px;
}
```
#### css sprites 
`CSS Sprites`其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的`background-image`，`background- repeat`，`background-position`的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。CSS Sprites为一些大型的网站节约了带宽，让提高了用户的加载速度和用户体验，不需要加载更多的图片
``` css
background-image: url(images/minibar.png);                /*显示小图*/
background-repeat: none;
background-position: 2px -55px; /*left top*/ /*定位小图*/
```

#### css清除浮动的几种方式
浮动：子盒子里使用了`float`浮动属性，导致父级对象盒子不能被撑开，这样CSS float浮动就产生了。副作用：背景不能显示；边框不能撑开；margin padding设置值不能正确显示
清除浮动的方式：
1. 对父级设置适合height
2. `clear: both`清除浮动：在父级结束前引入加入样式`clear: both`的<div>
3. 父级div定义`overflow: hidden`(BFC解决方案)
4. 父级div加class类，使用after伪元素清除浮动（推荐使用）
``` css
.clearfix:after{
    content:"";
    clear:both;
    display:block;
    height:0;
    overflow:hidden;
    visibility:hidden;
}
.clearfix{
    *zoom: 1;/*兼容 IE6，7 同样需要配合zoom使用，zoom缩放比，*号只有IE6-IE7执行，其他浏览器不执行*/
    }
```

#### BFC
[BFC](https://blog.csdn.net/DFF1993/article/details/80394150) 全称为 块格式化上下文 (Block Formatting Context) ，BFC理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。
应用场景或常见的作用：
1. 阻止外边距折叠
    - 问题案例：margin塌陷问题：在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。可以用overflow：hidden产生bfc来解决。
    - 解决办法：给item外面加一个div(样式加overflow:hidden或position:absolute)
2. 包含浮动元素
    - 问题案例：高度塌陷问题，在通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合，这时就可以用BFC来清除浮动了。
    - 解决办法：给父元素添加样式（overflow:hidden）
3. 阻止元素被浮动元素覆盖
    - 问题案例：div浮动兄弟这该问题：由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。
    - 解决办法：可以给右侧元素添加 overflow: hidden，触发BFC来解决遮挡问题。(这个方法可以用来实现两列自适应布局，效果不错，这时候左边的宽度固定，右边的内容自适应宽度。)

#### 常见定位方案
1. 普通流 (normal flow)
在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。
2. 浮动 (float)
在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。
3. 绝对定位 (absolute positioning)
在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。