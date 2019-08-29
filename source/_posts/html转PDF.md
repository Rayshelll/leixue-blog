---
title: html转PDF
date: 2019-08-15 12:54:45
tags: React
categories: 前端学习
---
### 方法一：[html2canvas](https://github.com/niklasvh/html2canvas) + [jspdf](https://github.com/mrrio/jspdf)
安装 `npm install html2canvas` `npm install jspdf`

<!-- more -->

``` js
// 引入 
import jsPDF from "jspdf";
import html2canvas from "html2canvas";

drawCanvas = () => {
    const element = document.getElementById("componentToPrint")!;
    const width = element.clientWidth;
    const height = element.clientHeight;

    // const canvas = document.createElement("canvas");
    const scale = 2;
    // canvas.width = width * scale;
    // canvas.height = height * scale;
    // canvas.style.width = `${width}px`;
    // canvas.style.height = `${height}px`;
    // const context = canvas.getContext('2d')!
    // const rect = element.getBoundingClientRect();//获取元素相对于视察的偏移量
    // context.scale(scale, scale);
    // context.translate(-rect.left,-rect.top);//设置context位置，值为相对于视窗的偏移量负值，让图片复位

    // console.log(rect.left, rect.top)
    // console.log(pageXOffset, pageYOffset)
    const opts = {
        width,
        height,
        dpi: window.devicePixelRatio * 2,
        scale,
        // canvas: canvas,
        windowHeight: document.body.scrollHeight,
        windowWidth: document.body.scrollWidth,
        x: pageXOffset,
        y: pageYOffset,
        useCORS: true,
    };
    html2canvas(element, opts)
        .then((canvas) => {
            const pageData = canvas.toDataURL("image/jpeg", 1.0); // 生成的图片地址
            // document.body.appendChild(canvas);
            const pdf = new jsPDF("", "pt", "a4");
            // addImage后两个参数控制添加图片的尺寸，此处将页面高度按照a4纸宽高比列进行压缩
            pdf.addImage(pageData, "JPEG", 0, 0, 595.28, 592.28 / canvas.width * canvas.height);
            pdf.save("billDetail.pdf");
            this.props.cb();
        });
}
```
### 方法二：[html2pdf](https://github.com/eKoopmans/html2pdf.js)
安装 `npm install html2pdf.js`
``` js
// 引入 
import html2pdf from "html2pdf.js";
drawPDF = () => {
    const element = document.getElementById("componentToPrint")!;
    const width = element.clientWidth;
    const height = element.clientHeight;
    // 导出配置
    const opt = {
        margin: 0,
        filename: "billDetail.pdf", // 输出pdf名字
        image: { type: "jpeg", quality: 1 }, // 导出的图片质量和格式
        html2canvas: {
            dpi: window.devicePixelRatio * 2,
            height, width,
            backgroundColor: null,
            scale: 2,
            windowHeight: document.body.scrollHeight, // 获取超出页面的内容
            windowWidth: document.body.scrollWidth,
            x: pageXOffset + 315, // 画布起点x坐标
            y: pageYOffset,
            useCORS: true // useCORS很重要，解决文档中图片跨域问题
        },
        jsPDF: { unit: "pt", format: "a4", orientation: "portrait" },
    };
    if (element) {
        html2pdf().set(opt).from(element).save(); // 导出
    }
}
缺点：画cavans时总不是从容器的(0, 0)坐标开始画，渲染出来会有偏差（具体原因跟我也不知道…………），使用`html2canvas`里的绘画参数`x`,`y`来调节
优点：比第一种方法渲染出来的清晰度高
```

遇到的坑：渲染总会有偏差，解决方法，查看他画画布的时候的`pageXOffset`和`pageYOffset`是否为0,0
查看包官方文档都可以在命令行`npm docs xx`