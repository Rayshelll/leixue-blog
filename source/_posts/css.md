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
        2. 父元素`display:flex; justify-content:center;`
        3. 父元素：`position:relative;` 
        子元素`{position:relative/absolute; left:50%; margin-left:-width(子元素)/2;}`（已知子元素宽高）
        3. 父元素：`position:relative;` 
        子元素：`position:relative/absolute; left:0; right:0; margin:auto;`
    - 垂直居中实现方式：    
        1. 父元素：`display:flex; align-items:center;`
        2. 父元素：`position:relative;` 
        子元素：`position:relative/absolute; top:50%; margin-top:-height(子元素)/2;`（已知子元素宽高）
        3. 父元素：`position:relative;` 
        子元素：`position:relative/absolute; top:0; bottom:0; margin:auto;`
    - 水平垂直居中实现方式：
        1. 父元素：`display:flex; justify-content:center; align-items:center;`
        2. 父元素：`display:flex;` 
        子元素：`margin:auto;`
        3. 父元素：`position:relative;` 
        子元素：`position:relative/absolute; top:50%; left:50%; margin-top:-height(子元素)/2;margin-right:-width(子元素)/2;`(已知块级元素的宽和高)
        4. 父元素：`position:relative` 
        子元素：`position:relative/absolute; top:0; left:0; bottom:0; right:0; margin:auto;` 

2. 行内元素：
    - `display:inline;`
    - a、b、span、img、input、strong、select、label、em、button、textarea（字体、input类、span）等；
    - 特性：
        1. 设置宽高无效；
        2. 对margin仅设置左右方向有效，上下无效；padding设置上下左右都有效，即会撑大空间；
        3. 不会自动进行换行；
    - 水平居中实现方式：父元素为块级元素
        1. 父元素`text-align:center`
    - 垂直居中实现方式：
        1. 子元素`line-height:height(父元素);`
        2. 父元素`display:table-cell; vertical-align:middle;`   
    - 水平垂直居中实现方式：           
        1. 父元素`display:table-cell; vertical-align:middle; text-align:center;`  
        2. 父元素`text-align:center` 子元素`line-height:height(父元素);`

3. 行内块状元素：
    - `display:inline-block;`
    - 特征：
        1. 不自动换行
        2. 能够识别宽高
        3. 默认排列方式为从左到右；(行内元素和块状元素都使用)

### css相对定位、绝对定位
1. 绝对定位(`position:absolute`)生成绝对定位的元素（脱离文档流），相对于 `static` 定位以外的第一个父元素进行定位(如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口)。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
2. 相对定位(`position:relative`)生成相对定位的元素(没有脱离文档流)，相对于自身正常位置进行定位。移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动.
3. 固定定位(`position:fixed`) 与`background-attachment:fixed;`属性功能相同。生成绝对定位的元素(脱离文档流)，相对于浏览器窗口进行定位。不受窗口大小变化和滚动条而改变位置
4. `position:static`默认值，没有定位，元素出现在正常的流中；`position:inherit`规定应该从父元素继承 position 属性的值。

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
    9. 伪类选择器(a:hover, li:nth-child)
- 可继承的样式：1.font-size 2.font-family 3.color 4.text-indent(首行文本的缩进)
- 不可继承的样式：1.border 2.padding 3.margin 4.width 5.height
- 优先级算法：
    1. 优先级就近原则，同权重情况下样式定义最近者为准;
    2. 载入样式以最后载入的定位为准;
    3. !important > 内联 > id > class > tag  
- CSS伪类：
    `p:first-of-type` 选择属于其父元素的首个`<p>`元素的每个`<p>`元素。
    `p:last-of-type ` 选择属于其父元素的最后`<p>`元素的每个 `<p>`元素。
    `p:only-of-type ` 选择属于其父元素唯一的`<p>`元素的每个`<p>`元素。
    `p:only-child `   选择属于其父元素的唯一子元素的每个`<p>`元素。
    `p:nth-child(2) ` 选择属于其父元素的第二个子元素的每个`<p>`元素。
    :first-child 与 :first-of-type的不同
    `:first-child` 匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素。
    `:first-of-type` 匹配的是该类型的第一个
    `:enabled `/ `:disabled` 控制表单控件的禁用状态。
    `:checked`  单选框或复选框被选中。
    `:before` / `:after` 定义对象之前/之后内容的样式
    `:first-letter` / `:first-line` 定义文本的第一个字符/首行样式 只能用于块级元素
    `:hover` / `:link` / `:focus` / `:visited` / `:active`
    

### 盒模型
1. 标准W3C盒子模型：
    1. width = content
    2. box-sizing:content-box(默认)
    3. 渲染wh受 padding border 等属性影响，动态大小
2. IE盒子模型中：
    1. width = content + padding + border；
    2. box-sizing:border-box；
    3. 渲染wh不受 padding border 等属性影响，固定大小

### Flex布局
**传统布局**基于盒状模型，依赖 `display`属性 + `position`属性 + `float`属性( 缺点：垂直居中等不好实现) 
**Flex**是Flexible Box的缩写，意为”弹性布局”
有两个重要概念：**容器**和**项目**(容器的子成员)
***注意***，设为Flex布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。

语法：
``` css
.box {
    display:flex;
    display:flex-inline; /* 行内元素flex布局 */
    display:-webkit-flex; /* 
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
    flex-direction:row(从左到右) / row-reverse (从右到左) / column (从上到下) / column-reverse(从下到上);
    flex-wrap:nowrap(默认值不换行)  / wrap(换行，第一行在上方)  / wrap-reverse(换行，第一行在下方) ;
    flex-flow:<flex-direction> <flex-wrap>;
    justify-content:flex-start(左对齐) / flex-end(右对齐)  / center (居中) / space-between(两端对齐)  / space-around(间隔相等);
    align-items:stretch(默认值，未设高度拉伸填满) / flex-start(起点对齐)  / flex-end (终点对齐) / center (中点对齐) / baseline(第一行文字的基线对齐);
    align-content:flex-start / flex-end / center / space-between / space-around / stretch;
}
```

#### 项目的属性
6个属性：
`order` 项目的排列顺序。数值越小，排列越靠前，默认为0
`flex-grow` 项目的放大比例，默认为0
`flex-shrink` 项目的缩小比例，默认为1
`flex-basis` 项目占据的主轴空间，优先级大于width
`flex` **前三个的简写，优先使用这个属性**
`align-self` 允许单个项目有与其他项目不一样的对齐方式,可覆盖容器属性align-items属性

``` css
.item {
    order:<integer>;
    flex-grow:<number>; /* default 0 */
    flex-shrink:<number>; /* default 1 负值对该属性无效*/
    flex-basis:<length> / auto; /* default auto */
    flex:none(0 0 auto) / auto(1 1 auto)/*默认值为0 1 auto*/
    align-self:auto / flex-start / flex-end / center / baseline / stretch; /*默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。*/
}
/* flex的不同取值 */
.item {flex:2333 3222 234px;}
.item {
    flex-grow:2333;
    flex-shrink:3222;
    flex-basis:234px;
}
.item {flex:1;}/*非负整数*/
.item {
    flex-grow:1;
    flex-shrink:1;
    flex-basis:0%;
}
.item-1 {flex:0%;}/*百分比*/
.item-1 {
    flex-grow:1;
    flex-shrink:1;
    flex-basis:0%;
}
.item-2 {flex:24px;}/*像素值*/
.item-1 {
    flex-grow:1;
    flex-shrink:1;
    flex-basis:24px;
}
.item {flex:2 3;}/*两个非负整数*/
.item {
    flex-grow:2;
    flex-shrink:3;
    flex-basis:0%;
}
.item {flex:2333 3222px;}/*一个非负整数 一个像素值*/
.item {
    flex-grow:2333;
    flex-shrink:1;
    flex-basis:3222px;
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
  flex:0 200px;
  background:blue;
}
.box2{
  flex:1;/*flex:auto*/
  background:red;
}
/*利用 float 配合 margin或overflow:hidden; 实现*/
.container{
  height:100px;
}
.box1{
  width:200px;
  float:left;
  background:blue;
  height:100%;
}
.box2{
  margin-left:200px;/* overflow:hidden;*/
  background:red;
  height:100%;
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
  background:blue;
  height:50px;
}
.box2{
  background:red;
  height:50px;
  width:200px;
}
```
#### css sprites 
`CSS Sprites`其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的`background-image`，`background- repeat`，`background-position`的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。CSS Sprites为一些大型的网站节约了带宽，让提高了用户的加载速度和用户体验，不需要加载更多的图片
``` css
background-image:url(images/minibar.png);                /*显示小图*/
background-repeat:none;
background-position:2px -55px; /*left top*/ /*定位小图*/
```

#### css清除浮动的几种方式
浮动：子盒子里使用了`float`浮动属性，导致父级对象盒子不能被撑开，这样CSS float浮动就产生了。副作用：背景不能显示；边框不能撑开；margin padding设置值不能正确显示
清除浮动的方式：
1. 对父级设置适合height
2. `clear:both`清除浮动：在父级结束前引入加入样式`clear:both`的<div>
3. 父级div定义`overflow:hidden`(BFC解决方案)
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
    *zoom:1;/*兼容 IE6，7 同样需要配合zoom使用，zoom缩放比，*号只有IE6-IE7执行，其他浏览器不执行*/
    }
```

#### BFC
[BFC](https://blog.csdn.net/DFF1993/article/details/80394150) 全称为 块格式化上下文 (Block Formatting Context)，BFC理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。
应用场景或常见的作用：
1. 阻止外边距折叠
    - 问题案例：margin塌陷问题：在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。可以用overflow：hidden产生bfc来解决。
    - 解决办法：给item外面加一个div(样式加overflow:hidden或position:absolute)
2. 包含浮动元素
    - 问题案例：高度塌陷问题，在通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合，这时就可以用BFC来清除浮动了。
    - 解决办法：给父元素添加样式（overflow:hidden）
3. 阻止元素被浮动元素覆盖
    - 问题案例：div浮动兄弟这该问题：由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。
    - 解决办法：可以给右侧元素添加 overflow:hidden，触发BFC来解决遮挡问题。(这个方法可以用来实现两列自适应布局，效果不错，这时候左边的宽度固定，右边的内容自适应宽度。)

#### 常见定位方案
1. 普通流 (normal flow)
在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。
2. 浮动 (float)
在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。
3. 绝对定位 (absolute positioning)
在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

#### css3新特性
其中最重要的 CSS3 模块包括：选择器、框模型、背景和边框、文本效果、2D/3D 转换、动画、多列布局、用户界面
1. 伪选择器：
`:last-child`选择器选择的是元素的最后一个子元素、
`:first-child`选择器选择的是元素的第一个子元素、
`:nth-child(n)`选择器用来定位某个父元素的一个或多个特定的子元素
`:nth-last-child(n)` CSS3 匹配父元素的倒数第n个子元素E
2. 字体@Font-face可以用来加载web字体样式
``` css
@font-face { 
font-family:myFont; 
src:url('Sansation_Light.ttf'); 
font-weight:bold;
}
div{
    font-family:myFont;
}
```
3. 文本效果：
    - text-shadow:5px 5px 5px #FF0000; 文字阴影
    - word-wrap:break-word; 自动换行，可拆分单词
    - text-outline:2px 2px #ff0000; 规定文本轮廓
4. 新背景属性：
    - background-clip	规定背景的绘制区域。	背景图片可以放置于 content-box、padding-box 或 border-box 区域
    - background-origin	规定背景图片的定位区域。 背景图片可以放置于 content-box、padding-box 或 border-box 区域	
    - background-size:x y(px/%)	规定背景图片的尺寸。
5. 边框属性：
    - border-image:url(border.png) 30 30 round;	设置所有 border-image-* 属性的简写属性。	
    - border-radius:25px;	设置所有四个 border-*-radius 属性的简写属性。	
    - box-shadow:10px 10px 5px #888888;	向方框添加一个或多个阴影。
6. `animation`动画复合属性：
    - animation-name 绑定绑定到选择器的 `@keyframes`的名称
    - animation-duration 规定完成动画所花费的时间，以秒或毫秒计
    - animation-timing-function 规定动画的速度曲线`liner` 默认`ease`
    - animation-delay 规定在动画开始之前的延迟
    - animation-iteration-count 规定动画应该播放的次数`infinite`
    - animation-direction 规定是否应该轮流反向播放动画
    ``` css
    .main:hover{
            animation:myanimations 2s ease 0s;<!-- 使用动画 -->
        }
        @keyframes myanimations {<!-- 定义动画名称 -->
            0%{   <!-- 和from状态一样 -->
                left:10px;
                opacity:1;
            }
            50%,70%{
                left:50%;
                opacity:.7;
                margin-left:-150px;
            }
            100%{ <!-- 和to状态一样 -->
                left:100%;
                opacity:0;
                margin-left:-300px;
            }
        }
    ```
7. `transform` :
- `transform` 2D转换效果：
    - 移动：translate(x,y) translateX/translateY
    - 旋转：rotate(angle)
    - 伸缩：scale(n,n) scaleX/scaleY
    - 斜切：skew(x-angle,y-angle) skewX/skewY
    - matrix(n,n,n,n,n,n)：需要六个参数，包含数学函数，允许您：旋转、缩放、移动以及倾斜元素
- `transform` 3D转换效果：
    - 移动：translate3d(x,y,z) translateX/translateY/translateZ
    - 旋转：rotate3d(x,y,z,angle) rotateX(angle)/rotateY(angle)/rotateZ(angle)
    - 伸缩：scale3d(n,n,n) scaleX/scaleY/scaleZ
    - matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)	定义 3D 转换，使用 16 个值的 4x4 矩阵。

8. `transition`过渡:
    - transition-property	规定应用过渡的 CSS 属性的名称。	
    - transition-duration	定义过渡效果花费的时间。默认是 0。	
    - transition-timing-function	规定过渡效果的时间曲线。默认是 "ease"。	
    - transition-delay	规定过渡效果何时开始。默认是 0。	
    ``` css
    div{
        transition:width 1s linear 2s;
        /* Firefox 4 */
        -moz-transition:width 1s linear 2s;
        /* Safari and Chrome */
        -webkit-transition:width 1s linear 2s;
        /* Opera */
        -o-transition:width 1s linear 2s;
    }
    ```
9. 用户界面：
    - resize：表示是否允许用户调整元素尺寸，允许：resize:both
    - box-sizing：表示盒模型:border-box还是标准模型:content-box(默认)
    - outline-offset：outline:2px solid red;outline-offset:15px;对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。轮廓与边框不同点：轮廓不占用空间、轮廓可能是非矩形
10. css3多列`column`：
    - column-count 规定列的数量`column-count:3;`
    - column-gap 规定列之间的间隔`column-gap:30px;`
    - column-rule 属性设置列之间的宽度、样式和颜色规则`column-rule:3px outset #ff0000;`

#### 完美的响应式布局vw+vh+rem
视口布局的优点：宽度和高度全部自动适应！再加上rem布局的字体适应
1. px 和 rem
em是相对长度单位。相对于当前对象内本文的字体尺寸
rem是相对于根元素<html>的相对字体大小，浏览器默认的字号16px，10px=10/16rem
``` css
html{
    font-size:20px;//1rem = 20px
}

html{
    font-size:(vw_fontsize / (vw_design / 2)) * 100vw; // vw_fontsize 可以设为75，vw_design为设计稿宽度
    @media only screen and (max-width:1600px) and (min-width:1280px){
        font-size:14px;
    }
    @media only screen and (max-width:1280px) and (min-width:960px){
        font-size:12px;
    }
    @media only screen and (max-width:960px){
        font-size:10px;
    }
}
```
2. vw、vh是基于视口的布局方案，故这个meta元素的视口必须声明。（解决宽高自动适配）
vw和vh是视口（viewport units）单位，何谓视口，就是根据你浏览器窗口的大小的单位
`<meta name="viewport" content="width=device-width,initial-scale=1.0">`
vw是可视窗口的宽度单位，和百分比有点一样，1vw = 可视窗口的宽度的百分之一，50vw代表了 此div占据视口宽度的50%、高度占据视口高度的20%，并且会随着视口的变化，进行自适应;

### CSS中 link 和@import 的区别是？
1. link属于HTML标签，而@import是CSS提供的;
2. 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
3. import只在IE5以上才能识别，而link是HTML标签，无兼容问题;
4. link方式的样式的权重高于@import的权重.
5. import规则一定要先于除了@charset的其他任何CSS规则

### CSS hack
CSS hack是通过在CSS样式中加入一些特殊的符号，让不同的浏览器识别不同的符号，以达到应用不同的CSS样式的目的。(不同浏览器识别不同css样式)
比如IE6能识别下划线“_”和星号“*”，IE7能识别星号“*”，但不能识别下划线”_ ”，而firefox两个都不能认识。
``` css
div {
    background:green;*background:red;
}
```
### 浏览器的内核分别是什么?
浏览器内核是测览器最核心的部分，负责对网页语法的解释并渲染网页(也就是显示网页效果)渲染引擎决定了浏览器如何显示网页的内容以及页面的格式信息。不同的浏览器内核对网页编写语法的解释不同，因此同一网页在不同内核浏览器中的渲染(显示)效果也可能不同。目前常见的浏览器内核有 Trident、 Gecko、 Webkit、 Presto、 Blink五种，5大浏览器基本采用的是单内核模式。主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。
1. 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机，负责生成DOM树，负责渲染和重绘。
2. JS引擎则：解析和执行javascript来实现网页的动态效果。

浏览器 | 内核
-|- 
IE | Trident |
Mozilla/Firefox | Gecko |
Safari/以前的Chrome | WebKit |
以前的Opera | Presto |
Chrome/Opera | Blink |

### 浏览器兼容问题
1. 不同浏览器的标签默认的外补丁(margin)和内补丁(padding)不同
解决方案：css里增加通配符*{ margin:0; padding:0;}
2. IE6双边距问题：在IE6中块级元素设置了float属性，同时又设置margin属性, 就会出现双边距问题，margin为以前的2倍
解决方案：给块级元素设置display:inline;`_display:inline;`，IE6能识别下划线“_”
3. 当标签的高度设置小于10px，在IE6、IE7中会超出自己设置的高度
解决方案：超出高度的标签设置`*overflow:hidden`，或者设置`*line-height`的值小于你的设置高度，IE6、IE7能识别“*”
4. 图片默认有间距
解决方案：使用float为img布局
5. IE9一下浏览器不能使用opacity
解决方案：
``` css
.name
{
    opacity:0.5; 
    filter:alpha(opacity = 50); 
    filter:progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);
}
```
6. 边距重叠问题：当相邻两个元素都设置了margin边距时，margin 将取最大值，舍弃最小值，BFC问题
解决方案：为了不让边重叠，可以给子元素增加一个父级元素，并设置父级元素为`overflow:hidden`
7. cursor:hand显示手型在safari上不支持
解决方案：统一使用`cursor:pointer`
8. 两个块级元素，父元素设置了`overflow:auto`，子元素设置了`position:relative`，且高度大于父元素，在IE6、IE7会被隐藏而不是溢出；
解决方案：父级元素设置`*position:relative`