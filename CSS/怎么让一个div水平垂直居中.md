# 怎么让一个div水平垂直居中？

```html
<div class="parent">
  <div class="child"></div>
</div>
```

```css
.parent {
      background: pink;
      width: 600px;
      height: 600px;
      margin: auto;
      margin-top: 50px;
}
.child {
      width: 200px;
      height: 200px;
      background: purple;
    }
```

方法1：定位

```css
.parent {
      position: relative;
    }
.child {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
    }
// 或
.parent {
      position: relative;
    }
 .child {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    }
```

方法2：flex弹性布局

```css
.parent {
    display: flex;
    justify-content: center;
    align-items: center;
}
// 或者
.parent{
  display:flex;
}
.child{
  margin:auto;
}
```

方法3：网格布局

```css
.parent {
    display: grid;
}
.child {
    justify-self: center;
    align-self: center;
}
```

方法4：伪元素法

```css
.parent {
    font-size: 0;
    text-align: center; 
}
.parent::before {
    content: "";
    display: inline-block;
    width: 0;
    height: 100%;
    vertical-align: middle;
}
.child{
  display: inline-block;
  vertical-align: middle;
}
```

方法5：

```
div.parent {
display: table;
}
div.child {
display: table-cell
vertical-align: middle;
text-align: center;
}
```

undefined：不明确的，也就是不知道用来干嘛的 （虽有无值）
not defined :  未定义的 (无中生有)