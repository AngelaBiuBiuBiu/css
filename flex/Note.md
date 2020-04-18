# Flex布局是什么？
Flex——Flexible Box，弹性布局。用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为Flex布局。
```
.box {
    display: flex;
}
```
行内元素也可以指定为Flex布局。
```
.inline-box {
    display: inline-flex;
}
```
设为flex布局以后，子元素的float、clear和vertical-align属性将失效。
## 基本概念
采用flex布局的元素，成为flex容器，它的所有子元素自动成为容器成员，称为flex项目。

容器默认存在两根轴：水平的主轴和垂直的交叉轴。主轴的开始位置叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列，单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。
## 容器的属性
### flex-direction
决定主轴的方向（即项目的排列方向）。

1. row（默认值）：主轴为水平方向，起点在左端
2. row-reverse：主轴为水平方向，起点在右端
3. column：主轴为垂直方向，起点在上沿
4. column-reverse：主轴为垂直方向，起点在下沿
### flex-wrap
默认情况下，项目都排在一条线（又称“轴线”）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

1. no-wrap（默认）：不换行
2. wrap：换行，第一行在上方
3. wrap-reverse：换行，第一行在下方
### flex-flow
flex-flow属性是flex-direction和flex-wrap属性的简写形式，默认值为row nowrap。
```
.box {
    flex-flow: <flex-direction> | <flex-wrap>
}
```
### justify-content
定义了项目在主轴上的对齐方式。具体对齐方向与主轴的方向有关。下面假设主轴从左到右：

1. flex-start（默认值）：左对齐
2. flex-end：右对齐
3. center：居中
4. space-between：两端对齐，项目之间的间隔都相等
5. space-around：每个项目两侧的间隔都相等，所有项目之间的间隔要比项目与边框之间的距离大一倍。
### align-items
定义项目在交叉轴上如何对齐。具体对齐方向与交叉轴的方向有关。下面假设主轴从上到下：

1. flex-start：交叉轴的起点对齐
2. flex-end：交叉轴的终点对齐
3. center：交叉轴的中点对齐
4. baseline：项目的第一行文字的基线对齐
5. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
### align-content
定义了多根轴线的对齐方式。如果该项目只有一条轴线，该属性不起作用。
1. flex-start：与交叉轴的起点对齐
2. flex-end：与交叉轴的终点对齐
3. center：与交叉轴的中点对齐
4. space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
5. space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍
6. stretch（默认值）：轴线占满整个交叉轴
## 项目的属性
### order
定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```
.item {
    order: <integer>;
}
```
### flex-grow
定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
```
.item {
    flex-grow: <number>;
}
```
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
### flex-shrink
定义项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
```
.item {
    flex-shrink: <number>;
}
```
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。
### flex-basis
定义在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值是auto，即项目的本来大小。
```
.item {
  flex-basis: <length> | auto;
}
```
它可以设为跟width和height属性一样的值，则项目将占据固定空间。
### flex
flex属性是flex-grow、flex-shrink和flex-basis的简写，默认值为0 1 auto。后两个属性可选。
```
.item {
    flex: none | <flex-grow> [<flex-shrink> || <flex-basis>]
}
```
该属性有两个快捷值，auto（1 1 auto）和none（0 0 auto）。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
### align-self
这个属性允许单个项目有与其他项目不同的对齐方式，可以覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```
.item {
    align-slef: auto | flex-start | flex-end | center | baseline | stretch;
}
```
该属性可能取6个值，除了auto，其他与align-items完全一致。