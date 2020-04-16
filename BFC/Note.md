# BFC——Block Formatting Context，块格式化上下文

# 视觉格式化模型
它是用来处理文档并将它显示在视觉媒体上的机制，也是CSS中的一个概念。

视觉格式化模型定义了盒的生成，盒主要包括了块盒、行内盒、匿名盒（没有名字不能被选择器选中的盒）以及一些实验性的盒（未来可能添加到规范中）。盒的类型由display属性决定。

## 块盒
### 1. 当元素的CSS属性display为block，list-item或table时，它是块级元素
### 2. 视觉上呈现为块，竖直排列
### 3. 块级盒参与BFC（块格式化上下文）
### 4. 每个块级元素至少生成一个块级盒，成为主要块级盒。一些元素比如`<li>`，生产额外的盒来放置项目符号，不过多数元素只生成一个主要块级盒。

## 行内盒
### 1. 当CSS的属性display的计算值为inline，inline-block或inline-table时，成为行内级元素
### 2. 视觉上它将内容与其他行内级元素排列为多行，典型的如段落内容，有文本或图片，都是行内级元素
### 3. 行内级元素生成行内级盒，参与行内格式化上下文（IFC），同时参与生成行内格式化上下文的行内级盒称为行内盒。所有display：inline的非替换元素生成的盒是行内盒。
### 4. 不参与生产格式化上下文的行内级盒成为原子行内级盒，这些盒由可替换元素，或display值为inline-block或inline-table的元素生成，不能拆分为多个盒。

## 匿名盒
匿名盒也有分匿名块盒和匿名行内盒，因为匿名盒没有名字，所以不能利用选择器来选择它们，所以它们的所有属性都为inherit或初始默认值。
```
<div>
    Some inline text                        // 匿名块盒来包含毗邻的行内级盒
    <p>followed by a paragraph</p>
    followed by more inline text.           // 匿名块盒来包含毗邻的行内级盒
</div>
```

# Formatting Context
它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位以及和其他元素的关系和相互作用。

最常用的formatting context有block formatting context（简称BFC）和inline formatting context（简称IFC）

# 三个定位方案
在定位的时候，浏览器会根据元素的盒类型和上下文对这些元素进行定位，可以说盒就是定位的基本单位。

定位时，有三种定位方案，分别是常规流，浮动和绝对定位。
## 1. 常规流
#### （1）在常规流中，盒一个接一个排列
#### （2）在块级格式化上下文里，它们竖着排列
#### （3）在行内格式化上下文里，它们横着排列
#### （4）当position为static或relative，并且float为none时会触发常规流
#### （5）相对于静态定位，position：static，盒的位置是常规里布局里的位置
#### （6）相对于相对定位，position：relative，盒偏移的位置由top、bottom、left、right属性定义，即使有偏移，仍然保留原有的位置，其他常规流不能占用这个位置

## 2. 浮动
#### （1）盒称为浮动盒
#### （2）它位于当前行的开头或末尾
#### （3）这导致常规流环绕在它的周边，除非设置clear属性

## 3. 绝对定位
#### （1）绝对定位方案，盒从常规流中被移除，不影响常规流的布局
#### （2）它的定位相对于它的包含块
#### （3）如果元素的属性为position：absolute或fixed时，它是绝对定位元素
#### （4）对于position：absolute，元素定位将相对于最近的一个relative、fixed或absolute的父元素，如果没有则相对于body
#### （5）对于position：fixed，当元素的祖先的transform、perspective或filter属性为非none时，容器由视口改为该祖先。

# 块格式化上下文
块格式化上下文（BFC）是页面CSS视觉渲染的一部分，用于决定块盒子的布局及浮动相互影响范围的一个区域。

## BFC的创建方法
### 1. 根元素或其他包含它的元素
### 2. 浮动元素（float值不为none）
### 3. 绝对定位元素（position为fixed或absolute）
### 4. 行内块元素（display：inline-block）
### 5. 表格单元格（display：table-cell，HTML表格单元格默认为该值）
### 6. 表格标题（display：table-caption，HTMl表格标题默认为该值）
### 7. 匿名表格单元格元素
元素的display为table、table-row、table-row-group、table-header-group、table-footer-group（分别是HTMl table、row、tbody、thead、tfoot的默认属性）或inline-block
### 8. overflow值不为visible的元素
### 9. display为flow-root的元素
### 10. contain值为layout、content、paint的元素
### 11. 弹性元素（display为flex或inline-flex元素的直接子元素）
### 12. 网格元素（display为grid或inline-grid元素的直接子元素）
### 13. 多列容器（元素的column-count或column-width不为auto，包括column-count为1）
### 14. column-span为all的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中

但其中，最常见的就是`overflow: hidden`、`float: left/right`、`position: absolute`。也就是说，每当看见这些属性的时候，就代表该元素已经创建了一个BFC了。

## BFC的范围
BFC包含创建该上下文元素的所有子元素，但不包括创建了新BFC的子元素的内部元素。也就是说，一个元素不能同时存在于两个BFC中。

BFC一个最重要的效果是，让处于BFC内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响，这是利用BFC清除浮动所利用的特性。

如果一个元素能够同时处于两个BFC中，那么就意味着这个元素能与两个BFC中的元素发生作用，就违反了BFC的隔离作用，所以这个假设就不成立了。

## BF的效果
BF最显著的效果就是建立一个隔离的空间，断绝空间内外元素间相互的作用。

BFC还有更多的特性：

1. 内部的盒会在垂直方向上一个接一个的排列（可以看作BFC中有一个常规的流）
2. 处于同一个BFC中的元素相互影响，可能会发生margin collapse
3. 每个元素的margin box的左边，与容器块border box的左边相接触（对于从左往右的格式化，否则相反）。即使存在浮动也如此
4. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然
5. 计算BFC的高度时，考虑BFC所包含的所有元素，连浮动元素也参与计算
6. 浮动盒区域不叠加到BFC上


>下面是4个示例（example1、example2、example3、example4），友情提醒：按顺序查看和学习～
