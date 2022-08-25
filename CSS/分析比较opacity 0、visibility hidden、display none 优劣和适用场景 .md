# 分析比较opacity: 0、visibility: hidden、display: none 优劣和适用场景 

1. display: none (不占空间，不能点击)（场景，显示出原来这里不存在的结构）

2. visibility: hidden（占据空间，不能点击）（场景：显示不会导致页面结构发生变动，不会撑开）

3. opacity: 0（占据空间，可以点击）（场景：可以跟transition搭配，展示动画效果）

   ## display:none

会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击

子元素随着父元素的消失一起消失不可见

性能：修改元素会造成文档回流,读屏器不会读取display: none元素内容，性能消耗较大

![image-20200907103557101](https://i.loli.net/2020/09/07/gNOd13psSDAnLhT.png)



## visibility: hidden

不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击

其子元素会继承该属性，随父元素一起隐藏，当子元素设置visibility：visible时，可显示子元素

性能：修改元素只会造成本元素的重绘,性能消耗较少读屏器读取visibility: hidden元素内容

![image-20200907103442940](https://i.loli.net/2020/09/07/VBDzUERfabtuveg.png)

## opacity: 0

不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击

子元素随父元素一起不可见，子元素设置opacity：1无效，仍然不可见

性能：修改元素会造成重绘，性能消耗较少

![image-20200907103732879](https://i.loli.net/2020/09/07/4SQPmtDzbJ1aldC.png)

## 测试代码：

style：

```css
div {
  margin: 0 auto;
  width: 200px;
  height: 200px;
  background-color: orange;
}
p {
  text-align: center;
  line-height: 200px;
  font-size: 20px;
  /*visibility: visible;*/
  /*display: block;*/
  /*opacity: 1;*/
}
```
html结构

```html
  <div>
    <p>子元素</p>
  </div>
```

js

```js
var div=document.getElementsByTagName('div');
setTimeout(()=>{
  div[0].style.display="none";
  // div[0].style.visibility="hidden";
  // div[0].style.opacity=0;
},3000)
div[0].onclick=()=>{
  console.log("可以点击");
}
```