# Flex布局

Flexbox 模块中的相关属性并不会改变屏幕阅读器对内容的读取顺序。

> 注意，HTML 中的可替代元素是无法成为 Flex 容器的，比如img、 input、 select等元素！

当一个元素变成了 Flex 容器之后，它的子元素，包括其伪元素 ::before 、::after 和 文本节点 都将成为 Flex 项目 。

在 Flexbox 布局中， Flex 容器和 Flex 项目之间的关系永远是父子关系.

> 注意，如果需要显式设置 Flex 容器尺寸的话，使用逻辑属性 inline-size 或 block-size 更符合多语言的 Web 布局！

Flexbox 布局中有一个强大的特性，当 Flex 容器有剩余空间时：

* 可以使用主轴的对齐方式 justify-content 来分配主尺寸的剩余空间；
* 可以使用侧轴的对齐方式 align-content 来分配侧尺寸的剩余空间。

也可以使用 flex 属性中的 flex-grow 按比例因子来扩展 Flex 项目的尺寸；当 Flex 容器是不足空间（Flex 项目溢出 Flex 容器），你可以使用 flex 属性中的 flex-shrink 按比例因子来对 Flex 项目进行收缩。

在使用 flex-direction 属性值 row-reverse 和 column-reverse 时，会对 Web 可访问性造成负面影响，因为该属性只是对视觉呈现进行重排，其对应的 HTML 文档的源码顺序是不受该属性影响的。

如果 Flex 容器没有足够多的空间，Flex 项目在溢出之前，每一个 Flex 项目将会尽可能缩小到其最小内容（min-content）的尺寸。即 Flex 项目一旦达到最小内容（min-content）大小， Flex 项目将开始溢出 Flex 容器 ！

order 初始值是 0 ，可以是正值，也可以是负值，属性值越大，越排在主轴的后面，反之越在主轴的前面。

## Flex属性分类

Flex属性可以分为两组：空间分配属性 和 对齐属性 。用于分配 Flex 容器空间的属性主要有：

* justify-content：沿 Flex 容器的主轴分配 Flex 容器的剩余空间；
* align-content：沿 Flex 容器的侧轴分配 Flex 容器的剩余空间；
* place-content：它是 justify-content 和 align-content 的简写属性。

* [对齐属性](./align.md)
* [空间分配属性](./space.md)
