# 已知img src=1.jpg style=width480px!important;”代码，如何修改才能让图片宽度为 300px ？注意下面代码不可修改

三种方法：

```htmlh
 <img src="1.jpg" style="width:480px!important; max-width: 300px">
  <img src="1.jpg" style="width:480px!important; transform: scale(0.625, 1);" >
  <img src="1.jpg" style="width:480px!important; width:300px!important;"> 
```

