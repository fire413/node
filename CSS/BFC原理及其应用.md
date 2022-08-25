# BFC原理及其应用

## BFC原理

块格式化上下文（Block Formatting Context,BFC)是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

**具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。**

通俗一点来讲，可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

触发BFC的条件：

- 根元素（`<html>`)
- 浮动元素（元素的`float`不是`none`）
- 绝对定位元素（元素的`position`为`absolute`或`fixed`）
- 行内块元素（元素的`display`为`inline-block`）
- 表格单元格（元素的`display`为`table-ceil`，HTML表格单元格默认为该值）
- 表格标题（元素`display`为`table-caption`，HTML表格标题默认为该值）
- 匿名表格单元格元素（元素的`display`为`table`、`table-row`、`table-row-group`、`table-header-group`、`table-footer-group`(分别为HTML `table`、`row`、`tbody`、`thead`、`tfoot`的默认属性)或`inline-block`）
- `overflow`值不为`visible`的块元素
- `display`值为`flow-root`的元素
- `contain`值为`layout`、`content`或`paint`的元素
- 弹性元素（`display`为`flex`或`inline-flex`元素的直接子元素）
- 网格元素（`display`为`flex`或`inline-grid`元素的直接子元素）
- 多列容器（元素的`column-count`或`column-width`部位`auto`，包括`column-count`为1）
- `column-span`为`all`的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中

## BFC的应用

**1.同一个BFC下外边距会发生折叠**

```html
<head>
    <style>
div{
    width: 100px;
    height: 100px;
    background: lightblue;
    margin: 100px;
}
        </style>
</head>
<body>
    <div></div>
    <div></div>
</body>
```

![](https://i.loli.net/2020/09/04/QLn4ivlTBcm3My8.png)

**2.BFC可以包含浮动的元素（清除浮动）**

```html
<div style="border: 1px solid #000;overflow: hidden">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

![](https://i.loli.net/2020/09/04/xiOj7eWnb8dpraf.png)

**3.BFC可以阻止元素被浮动元素覆盖**

```html
<div style="height: 100px;width: 100px;float: left;background: lightblue">我是一个左浮动的元素</div>
<div style="width: 200px; height: 200px;background: #eee; overflow:hidden;">我是一个没有设置浮动, 
也没有触发 BFC 元素, width: 200px; height:200px; background: #eee;</div>
```

![](https://i.loli.net/2020/09/04/z1HUFIGpdy53XMs.png)

## 其他：

**IFC（Inline formatting contexts）：内联格式上下文** IFC的line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响)IFC中的line box一般左右都贴紧整个IFC，但是会因为float元素而扰乱。float元素会位于IFC与与line box之间，使得line box宽度缩短。 同个ifc下的多个line box高度会不同 IFC中时不可能有块级元素的，当插入块级元素时（如p中插入div）会产生两个匿名块与div分隔开，即产生两个IFC，每个IFC对外表现为块级元素，与div垂直排列。 那么IFC一般有什么用呢？ 水平居中：当一个块要在环境中水平居中时，设置其为inline-block则会在外层产生IFC，通过text-align则可以使其水平居中。 垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中。

**GFC（GrideLayout formatting contexts）：网格布局格式化上下文** 当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。那么GFC有什么用呢，和table又有什么区别呢？首先同样是一个二维的表格，但GridLayout会有更加丰富的属性来控制行列，控制对齐以及更为精细的渲染语义和控制。

**FFC（Flex formatting contexts）:自适应格式上下文** display值为flex或者inline-flex的元素将会生成自适应容器（flex container），可惜这个牛逼的属性只有谷歌和火狐支持，不过在移动端也足够了，至少safari和chrome还是OK的，毕竟这俩在移动端才是王道。Flex Box 由伸缩容器和伸缩项目组成。通过设置元素的 display 属性为 flex 或 inline-flex 可以得到一个伸缩容器。设置为 flex 的容器被渲染为一个块级元素，而设置为 inline-flex 的容器则渲染为一个行内元素。伸缩容器中的每一个子元素都是一个伸缩项目。伸缩项目可以是任意数量的。伸缩容器外和伸缩项目内的一切元素都不受影响。简单地说，Flexbox 定义了伸缩容器内伸缩项目该如何布局。