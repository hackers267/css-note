# Web布局

css中有不同的容器。它主要由 CSS 的 display 属性的值来决定，比如：

* block 时称为块容器；
* inline 时称为内联容器；
* flex 或 inline-flex 时称为Flexbox容器；
* grid 或 inline-grid 时称为 Grid 容器（网格容器）。

随着 CSS Flexbox 特性出现之后，CSS 新增了像 justify-content 、align-content 、align-items 、justify-items 和 justify-self 以及 align-self 等属性，用来控制 Web 布局上的对齐方式。最初这些属性是在 Flexbox 相关规范中定义的，但随着 CSS Grid 布局出现之后，W3C 的 CSS 工作组将这些属性单独划分到一个模块中，即 CSS Box Alignment 模块。

* [Flex布局](./flex/ReadMe.md)
    * [对齐属性](./flex/align.md)
