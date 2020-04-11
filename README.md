# css

## 水平居中
### 1. 行内元素：父元素设置text-align为center
### 2. 单个块级元素：块级元素margin-left和margin-right为auto
### 3. 多个块级元素
#### 3.1 每个块级元素设置display为inline-block，再利用行内元素的居中方法即可
#### 3.2 多个块级元素的父元素的display设置为flex，justify-content:center即可