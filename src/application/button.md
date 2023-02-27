# 自定义Button按钮

本节内容关于如果创建一个跨平台，可访问性良好，可以主题定制和配置的`Button`按钮。`Button`按钮不仅仅是指`button`
，而且还包括`a`按钮。

## 基本的`html`结构

这里是为了定义`Button`的样式，为了防止出现其他的行为，我们通过`html`把`button`和`a`的预定义行为屏蔽。所有`html`结构如下：

```html
<a href="javascript:void(0);">Button</a>
<button type="button">Button</button>
```

## 重置样式

在重置其他的样式之前，我们先重置`box-sizing`样式，方便我们在css盒模式计算上的一致性。

```css
* {
    box-sizing: border-box;
}
```

### 重置`a`标签样式

`a`标签有一个预定义的`text-decoration`样式，因为我们要把它修改为统一的按钮样式，所有我们需要把这个样式重置：

```css
a.button {
    text-decoration: none;
}
```

`a`标签样式的重置（只是去除了下划线）还是比较简单的，接下来就是来重置`button`标签的样式了。

相对于`a`标签只需要重置`text-decoration`，`button`标签需要重置更多的样式：

* border
* padding
* cursor
* background-color等

```scss
button.button {
  border: none;
  background-color: transparent;
  padding: 0;
  font-family: inherit;
  cursor: pointer;

  @media screen and (-ms-high-contrast: active) {
    border: 2px solid currentColor;
  }
}
```

在重置`button`标签的样式的时候，我们不仅仅重置了在一般模式下的样式，而且添加了在高对比度的模式下，`button`的`border`样式。这样的设计可以使得`button`的可访问性更佳。

## 设置display样式

接下来，我们再看看`display`样式的选择，考虑到`Button`中文字的对齐和后面对`icon`的支持，我们选择使用`inline-flex`。

```scss
a.button,
button.button{
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

## 设置可视化样式

下面，我们就来看看`Button`最基本的可视化样式应该是什么样的：
```scss
:root{
  --button-color: #3eb6ff;
}

a.button,
button.button{
//  ...exiting styles
  backgound-color: var(--button-color);
  color: #fff;
  border-radius: 8px;
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.18);
}
```

### 大小

```scss
a.button,
button.button{
  // ... existing styles
  padding: 0.25em 0.75em;
  min-width: 10ch;
  min-height: 44px;
}
```

在设置`padding`时，我们使用了`em`作为单位，这样可以使得在`Button`中字体大小改变的时候，其内间距可以保持一个合理的值。

同时，我们在设置`min-width`的时候，使用了`ch`作为单位(`ch`为相对单位，具体见[值和单位](../base/value_unit.md))。这里更多的是考虑到在一个文本内容多和文本内容少，比如在*保存*和*导出为Excel*时，两者之间的对比不至于太大而显得突兀。 

设置`min-height`是考虑到在触屏设置上按钮的大小显示。

### 文本样式

在设置文本样式中，我们重点是关注文本的对齐和行高。在这里我们要使用`text-align`控制文本居中对齐。

```scss
a.button,
button.button{
  // ... existing styles
  text-align: center;
  line-height: 1.1;
}
```

### 状态样式

[//]: # (添加按钮的状态样式：hover,focus和active)
