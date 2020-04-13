定位的原理很简单，利用定位，可以准确的定义元素框，相对于其正常位置、父元素、另一个元素甚至浏览器窗口本身的位置，应该出现在哪里。

position: static | relative | absolute | fixed | sticky | inherit

# static（默认值）
如果省略position，浏览器默认该元素是static定位。

这时，浏览器会按照源码的顺序，决定每个元素的位置，这称为"正常的页面流"。也就是说，static定位所导致的元素位置，是浏览器自主决定的，所以这时候top、left、right、bottom这四个值，以及z-index无效。
# relative（不脱离文档流）
relative表示相对于默认位置（即static时的位置）进行偏移，也就是说，定位的基点是元素的默认位置。

该关键字下，元素先放置在未添加定位时的位置，在不改变页面布局的前提下调整元素位置，因为会在此元素未添加定位时所在位置留下空白。

必须搭配top、bottom、left、right这四个属性一起使用，用来指定偏移的方向和距离。

对table-*-group、table-row、table-column、table-cell、table-caption元素无效。
# absolute（脱离文档流）
元素会被移出正常的文档流，不为元素预留空间，通过指定元素相对于最近的非static定位的祖先元素的偏移来确定元素的位置。若不存在这样的祖先元素，则定位的基点就会变成整个网页的根元素html。

绝对定位的元素可以设置外边距（margins），不会与其他边距合并。

absolute也必须搭配top、bottom、left、right这四个属性使用。
# fixed（脱离文档流）
通过指定元素相对于屏幕视口（viewport，浏览器窗口）的位置来指定元素的位置。也就是说，定位的基点是浏览器窗口，这就导致元素的位置不会随着页面的滚动而滚动，就像固定在页面上一样。

它如果搭配top、bottom、left、right使用，表示元素的初始位置是基于视口计算的，否则初始位置就是元素的默认位置。

fixed属性会创建新的层叠上下文。

当元素的祖先的transform、perspective或filter属性为非none时，容器由视口改为该祖先。
# sticky（不脱离文档流）
元素根据正常文档流进行定位，然后相对它的最近滚动祖先和containing block（最近块级祖先），包括table-related元素，进行偏移。

sticky是relative和fixed的结合。sticky生效的前提是搭配top、bottom、left、right使用，不能省略，否则就等同于relative定位，不产生动态固定的效果。因为这四个属性是用来定义偏移距离的。

它的具体规则是，当页面滚动，父元素开始脱离视口时（即部分不可见），只要与sticky元素的距离达到生效门槛，relative定位自动切换为fixed定位；等到父元素完全脱离视口时（即完全不可见），fixed定位自动切换回relative定位。

一个sticky元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上（当该祖先的overflow是hidden、scroll、auto或overlay时），即便这个祖先不是真的滚动祖先。这个阻止了所有“sticky”行为。