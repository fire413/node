# 如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性

```html
<style>
    div {
      width: 200px;
      height: 100px;
      margin: 0 auto;
      box-shadow: 10px 10px 5px #888;
      background-color: pink;
    }
  </style>

<div>
    如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性
  </div>
```

## 单行：

```css
div {

overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;

}
```

![image-20200908103228503](https://i.loli.net/2020/09/08/3lML76uNfsKzDH4.png)

## 多行：

```css
div {

display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 5; //行数
overflow: hidden;

}
```

![image-20200908103358346](https://i.loli.net/2020/09/08/sknItFPd9LlJ1aS.png)

注意：有缺陷，最后一行有可能出现指展示半行的情况

## js实现多行文本溢出：

```js
const div = document.querySelector('div')

let words = div.innerHTML.split(/(?<=[\u4e00-\u9fa5])|(?<=\w*?\b)/g)
while (div.scrollHeight > div.clientHeight) {
  words.pop()
  div.innerHTML = words.join('') + '...'
}
```

![image-20200908110848570](https://i.loli.net/2020/09/08/w1n6oxVKPOaNBX9.png)