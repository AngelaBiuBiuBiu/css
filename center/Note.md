# 居中

## 水平居中
### 1. 行内元素：父元素设置text-align为center
### 2. 单个块级元素：块级元素margin-left和margin-right为auto
### 3. 多个块级元素
#### 3.1 每个块级元素设置display为inline-block，再利用行内元素的居中方法即可
#### 3.2 多个块级元素的父元素的display设置为flex，justify-content:center即可


## 垂直居中
### 1. 行内元素
#### 1.1 单行
##### （1）有时候行内元素或者文字显示为垂直居中，仅仅是因为它们的上下内边距相等
##### （2）若出于某些原因padding不能用，而你又需要将一些不换行的文字垂直居中，你可以使文字的line-height和height的值相等
#### 1.2 多行
##### （1）上边距和下边距相等
##### （2）设置文字所在的元素为一个table cell，不管它本来就是table还是你用css使这个元素表现的像一个table cell，若为css设置的表格表现，则使用vertical-align:middle
##### (3) 使用flexbox，单个flex子元素可以非常轻易的被一个flex的父元素垂直居中，但是这种方法只适合父容器有固定高度的！！！
##### (4) 一个完整高度的伪元素放置在容器内，并与文本垂直对齐
## 2. 块级元素
### 2.1 已知元素的高度：使用绝对定位
### 2.2 未知元素的高度
#### （1）transform
#### （2）如果你不介意元素是否拉伸了容器的高度，你还可以使用table或CSS display将元素放入表格即可
#### （3）flex布局



## 水平垂直居中
### 1. 知道元素的宽高：负margin法 + absolute
### 2. 不知道元素宽高
#### (1) transform
#### (2) display:table-cell
### 万能法：flex布局
### 针对一个元素特别好用：grid配合margin
