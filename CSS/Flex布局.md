# Flex布局

## 什么是Flex布局？

Flex是Flexible Box的缩写，意为“弹性布局”，用来为盒状模型提供最大的灵活性。任何一个容器都可以使用Flex布局。

注意：设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

## 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![img](https://i.loli.net/2020/09/24/3ZqQTceGxi1mKaF.png)

## 容器属性

有一下六个属性：

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

### flex-direction

决定主轴方向，即项目排列方向。

```css
.box {
	flex-direction: row|row-reverse|column|column-reverse;
}
```

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。



## 项目属性