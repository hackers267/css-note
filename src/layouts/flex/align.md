# flex布局中的对齐属性

用于在 Flexbox 布局中对齐的属性如下：

* align-self：沿 Flex 容器侧轴对齐单个 Flex 项目；
* align-items：将所有 Flex 项目作为一个组，沿 Flex 容器侧轴对齐。

## justify-content属性

justify-content 取值为 flex-start 、flex-end 和 center 时，相当于：

* flex-start ：主轴起点对齐（ltr 模式是左对齐）；
* flex-end ：主轴终点对齐（ltr 模式是右对齐）；
* center ：主轴居中对齐。

justify-content 属性设置为 space-around 、space-between 或 space-evenly ，在 Flex 项目之间分配 Flex 容器的剩余空间。

* space-between 会让行上第一个 Flex 项目的起始边缘与 Flex 容器主轴起点相吻合，行上最后一个 Flex 项目的结束边缘与 Flex 容器主轴终点相吻合，其它相邻 Flex 项目之间间距相等。当 Flex 容器中只有一个 Flex 项目时，其表现行为和 flex-start 等同。
* space-around 会让行上第一个 Flex 项目的起始边缘与 Flex 容器主轴起点间距，和行上最后一个 Flex 项目的结束边缘与 Flex 容器主轴终点间距相等，并且等于其他相邻两个 Flex 项目之间间距的二分之一。当 Flex 容器中只有一个 Flex 项目时，其表现行为和 center 等同。
* space-evenly 会让行上第一个 Flex 项目的起始边缘与 Flex 容器主轴起点间距，和最后一个 Flex 项目的结束边缘与 Flex 容器主轴终点间距相等，并且等于其他相邻两个 Flex 项目之间间距。当 Flex 容器中只有一个 Flex 项目时，其表现行为和 center 等同。

如果 Flex 容器没有额外的剩余空间，或者说剩余空间为负值时， justify-content 属性的值表现形式:

* flex-start 会让 Flex 项目在 Flex 容器主轴终点处溢出 ；
* flex-end 会让 Flex 项目在 Flex 容器主轴起点处溢出；
* center 会让 Flex 项目在 Flex 容器两端溢出；
* space-between 和 flex-start 相同；
* space-around 和 center 相同；
* space-evenly 和 center 相同；
* start 和 flex-start 相同；
* end 和 flex-end 相同。

## align-content属性

要是在 Flex 项目上显式设置了其高度（height 或 block-size）时，即使 align-items 的值为 stretch ，也不会拉伸 Flex 项目。

当 Flex 容器中，所有行的尺寸之和大于 Flex 容器侧轴尺寸（即 Flex 容器侧轴方向没有剩余空间 ）时，align-content 属性值表现行为：

* flex-start 会让 Flex 容器的行在侧轴结束点溢出；
* flex-end 会让 Flex 容器的行在侧轴起点溢出；
* center 会让 Flex 容器行在侧轴两端溢出；
* stretch 表现行为类似于 flex-start；
* space-around 表现行为类似于 center；
* space-between 表现行为类似于 flex-start；
* space-evenly 表现行为类似于 center。

虽然在 Flexbox 布局中，无法在 Flex 容器的主轴上，直接使用 justify-self 和 justify-items 将 Flex 项目从一个组中分离出来，但我们可以在 Flex 项目中使用 margin: auto 将 Flex 项目在 Flex 容器的主轴上进行分组。

为了应对现有的Flex布局中，因对齐溢出导致的内容丢失问题，在` CSS Box Alignment Module Level 3 `中添加了安全对齐，安全对齐属性新增了 safe 和 unsafe 两个关键词：

* safe关键字会将因为对齐方式导致溢出时，将设置的对齐模式切换到 start 对齐模式下，目的是避免“数据丢失”，其中部分项目超出对齐容器的边界并且无法滚动到。
* unsafe，即使会导致此类数据丢失，也会遵守对齐方式。
