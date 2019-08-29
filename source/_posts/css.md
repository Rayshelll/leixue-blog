---
title: css
date: 2019-08-19 16:10:39
tags: CSS
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
        1. `{margin:0 auto;}`
        2. `{position: relative/absolute; left: 50%;}`
    - 垂直居中实现方式：    
        1. 父元素：`display: flex;` 子元素：`align-items: center;`
        2. 父元素：`position: relative;` 子元素：`position: absolute; top: 50%;margin-top=-height（子）/2;`
        3. 父元素：`position: relative;` 子元素：`position:absolute; top:0; bottom:0;margin:auto;`
    - 水平垂直居中实现方式：
        1. 父元素：`position: relative; ` 子元素：`position: absolute; top: 50%; left: 50%; margin-top=-height（子）/2; margin-right=-width/2;(已知块级元素的宽和高)`
        2. 父元素：`position:relative` 子元素：`position: absolute; top:0; left:0; bottom:0; right:0; margin:auto;`
        3. 父元素：`display:flex; `子元素：`margin:auto;`
<!-- more -->
2. 行内元素：
    - `display:inline;`
    - a、b、span、img、input、strong、select、label、em、button、textarea（字体、input类、span）等；
    - 特性：
        1. 设置宽高无效；
        2. 对margin仅设置左右方向有效，上下无效；padding设置上下左右都有效，即会撑大空间；
        3. 不会自动进行换行；
    - 水平居中实现方式：
        1. 通过给父元素设置 `text-align:center`
    - 垂直居中实现方式：
        1. 子元素`line-height:父height;`
        2. 父元素`display: table-cell;vertical-align:middle;   `               
3. 行内块状元素：
    - `display:inline-block；`
    - 特征：
        1. 不自动换行
        2. 能够识别宽高
        3. 默认排列方式为从左到右；(行内元素和块状元素都使用)

### css相对定位、绝对定位
1. 绝对定位(`position:absolute`)脱离文档流，left、right、top、bottom属性相对于其最接近的一个具有定位属性的父包含块进行绝对定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口。
2. 相对定位(`position:relative`)没有脱离文档流，以static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动.
3. 固定定位(`position: fixed`) 与`background-attachment:fixed;`属性功能相同。不受窗口大小变化和滚动条而改变位置
4. 嵌套使用：子容器在父容器底部居中：父容器：`position：relative；`子容器：p`osition：absolute；bottom：0；left：0；right：0；margin: auto`

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
    2. box-sizing: content-box；
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
```