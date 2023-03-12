# 尺寸属性和属性值

CSS 中设置元素尺寸，主要由 尺寸属性 和 尺寸属性值 两部分来决定，只不过，这两部分所涉及到的内容比较多。

比如说，在 CSS 中给一个元素设置尺寸时，常会使用 width 、height 、inline-size 和 block-size ，也会使用 min-width 、min-height 、min-inline-size 、min-block-size 、max-width 、max-height 、max-inline-size 和 max-block-size 给元素限定一个尺寸。但要最终决定元素尺寸大小的是这些属性的值.

* auto：设置值为 auto 时，容器的大小将会以容器上下文来计算。如果它是个块元素，等于父容器宽度，如果它是个内联元素，则等于元素内容的尺寸大小；不过给 min-width、min-height、min-inline-size 或 min-block-size 设置值为 auto 时，将会指定一个自动计算好的最小值 。
* none：如果取值为 none 时，元素盒子的大小是没有任何限制的。
* <length-percentage>：使用 <length> 或 <percent> 指定元素的大小。其中 <length> 是一个长度值，它可能是一个固定长度值，也可能是一个相对长度值，主要取决于其单位，比如 px 是一个固定值，vw 和 rem 又是一个相对值。<percent> 是一个百分比值，根据其父元素的宽度来解析百分比。
* min-content：如果指定了内联轴，那么 min-content 对应的大小则是内联大小，否则将表现为属性的初始值，即固有的最小宽度。
* max-content：如果指定了内联轴，那么 max-content 对应的大小则是内联大小，否则将表现为属性的初始值，即固有的首选宽度。
* fit-content()：如果显式指定了内联轴，使用 fit-content() 函数，可以用指定的参数替换可用空间，即 min(max-content, max(min-content, <length-percentage>))；否则将表现为属性的初始值。对于内在尺寸，fit-content(<length>) 表现长度值（<length>）。如果 fit-content() 使用了百分比值，min-content 作为最小内容，max-content 作为最大内容 。

> `auto` 、`min-content` 、`max-content` 和 `fit-content()` 又被称为自动计算尺寸大小方式。

