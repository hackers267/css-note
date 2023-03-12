# 空间分配

要分配空间，首先浏览器必须确定有多少空间可用 。一般情况，浏览器会按照下面的过程来分配空间。

* 计算 Flex 容器内的可用空间 。Flex 容器的可用空间指的是 Flex 容器的主轴尺寸（Main Size）减去其 内距（padding） 、 边框宽度（border-width） 、间距（gap） 和 Flex 项目的外边距（margin） 。
* 计算每个 Flex 项目的伸缩基础大小和假设的主尺寸 ，即使用 flex-basis 、min-width 、min-inline-size 、width 、 inline-size 或 Flex 项目内容大小（min-content 或 max-content）设定的大小。其中 flex-basis 是 Flex 项目所需的最小尺寸，假设的主尺寸是指应用伸缩因子之前 Flex 项目的尺寸。而且 Flex 项目的伸缩基础大小永远不会小于其内容的伸缩基础大小。
* 计算所有 Flex 项目的总假设主尺寸 。
* 将所有 Flex 项目的假想主尺寸与 Flex 容器的可用空间进行比较 。当所有 Flex 项目的假想主尺寸总和大于 Flex 容器可用空间时，将会使用 flex-shrink 属性值作为 Flex 项目的收缩因子（收缩比率）来收缩 Flex 项目；当所有 Flex 项目的假想主尺寸总和小于 Flex 容器可用空间时，将会使用 flex-grow 属性值作为 Flex 项目的扩展因子（扩展比率）来扩展 Flex 项目。

也就是说，使用 Flexbox 布局时，浏览器会使用伸缩因子（包括扩展因子和收缩因子）决定从每个 Flex 项目中增加（扩展因子）或减去（收缩因子） Flex 容器的剩余空间，并且浏览器在循环中完成每个 Flex 项目的计算。


## flex项目


Flexbox 模块中的 flex-basis 属性（flex 简写属性成员之一） 也可以用来设定 Flex 项目的大小。而且它还会受 flex 属性中的 flex-grow 和 flex-shrink ，以及Flex 容器的可用空间、剩余空间和不足空间等因素影响。

每一个 Flex 项目因未显式设置任何与尺寸有关的属性，浏览器视每一个 Flex 项目的尺寸即为其内容的最大尺寸（max-content），同时浏览器根据内容多少，可计算出其宽度的具体值是多少像素值。

### flex属性

flex的默认值为`flex: 0 1 auto`。即：

* flex-grow:0, flex项目不扩展
* flex-shrink:1, flex项目收缩
* flex-basis:auto flex项目的默认尺寸为项目内容尺寸(`max-content`)

flex 属性的单值语法时，其值必须为以下其中之一：

* 一个无单位的数值（*\<number>*），比如 flex: 1 ，这个时候它（即1）会被当作 flex-grow 属性的值；
* 一个有效的长度值（*\<length-percentage>* ），比如 flex: 30vw ，这个时候它（即 30vw）会被当作 flex-basis 属性的值；
* 关键词 none 、 auto 或 initial （即初始值）。

flex 属性的双值语法，其第一个值必须为 一个无单位的数值（*\<number>*） ，并且它会被当作 flex-grow 属性的值 ；第二个值必须为以下之一：

* 一个无单位的数值（*\<number>*），它会被当作 flex-shrink 属性的值；
* 一个有效的长度值（*\<length-percentage>*），它会被当作 flex-basis 属性的值。

flex 属性的三值语法：

* 第一个值必须是一个无单位的数值（*\<number>*），并且它会被当作 flex-grow 属性的值；
* 第二个值必须是一个无单位的数值（*\<number>*），并且它会被当作 flex-shrink 属性的值；
* 第三个值必须是一个有效的长度值（*\<length-percentage>*），并且它会被当作 flex-basis 属性的值。

属性别名：

* `flex:auto`属性相当于:`flex: 1 1 auto`;
* `flex:initial`属性相当于：`0 1 auto`;
* `flex:none`属性相当于:`flex: 0 0 auto`;

如果要真的实现所有 Flex 项目宽度相等，除了在 Flex 项目上设置为 flex:1 之外，还需要显式设置 min-width 值为 0;

在大多数情况下，在 Flex 项目上设置 flex 属性时，其常见值的效果有：

* flex: 0 auto 和 flex: initial ，这两个值与 flex: 0 1 auto 相同，也是 flex 的初始值 。会根据 Flex 项目的 width (或 inline-size) ，和 height （或 block-size）属性值来决定 Flex 项目尺寸。当 Flex 容器有剩余空间时，Flex 项目并不会扩展填满整个 Flex 容器，但当 Flex 容器有不足空间时，Flex 项目会收缩到其最小值，即 min-content 。
* flex: auto 和 flex: 1 1 auto 相同。Flex 项目会根据 width（或 inline-size），和 height（或 block-size）来决定大小，但是完全可以扩展 Flex 容器剩余的空间。
* flex: none 和 flex: 0 0 auto 相同。 Flex 项目会根据 width（或 inline-size） ，和 height (或 block-size) 来决定大小，但是完全不可伸缩。
* flex: *\<positive-number>*（正数）和 flex: 1 0px 相同。Flex 项目可伸缩，并将 flex-basis 值设置为 0 （需要带有效的 *\<length>* 或 *\<percentage>* 单位），导致 Flex 项目会根据设置的比例因子来计算 Flex 容器的剩余空间。Flex 项目按比例扩展或收缩。

### flex子属性

* *\<flex-grow>* ：定义 Flex 项目的 flex-grow 属性的值，取值为 *\<number>*。
* *\<flex-shrink*> ：定义 Flex 项目 flex-shrink 属性的值，取值为 *\<number>* 。
* *\<flex-basis>* ：定义 Flex 项目的 flex-basis 属性的值。若值为0时，则必须加上单位（*\<length>*或*\<percentage>*），比如0px或0%，避免被视作伸缩性flex-grow或flex-shrink的值。


