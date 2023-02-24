# 自定义Radio按钮

在这里，我们会自定义一个**跨平台**,**可变大小**,**主题定制**的纯CSS实现的Radio按钮。

在这个实现中，我们会应用到以下几个主要的CSS属性：

* em 用于改变大小
* appearance: none 用于可访问性
* Grid 用于样式布局
* currentColor 用于样式定制

> 需要注意的是，在这里我们默认认为`css`代码都会通过`autoprefixer`进行处理，所以属性将不加`-webkit-`和`-moz-`等前缀
## Radio的Html结构

在使用`Radio`的时候，我们通常会使用下面两种结果：

```html
<label>
    <input type="radio" name="radio"/>
    Radio label test
</label>
```

或

```html
<input type="radio" name="radio" id="radio"/>
<label for="radio">Radio label text</label>
```

这里使用提到的技术对于上面的两种html结构都适用，不过为了避免使用额外的`div`包装。在这里的示例中，我们选择使用第一种结构。下面的示例中，我们以下面的html结构为基础：

```html
<label class="form-control">
    <input type="radio" name="radio"/>
    Radio
</label>
<label class="form-control">
    <input type="radio" name="radio"/>
    Radio - checked
</label>
```

这里的`html`结构中出现了两个`radio`元素的原因是，我们需要在开发的过程中对比选中和非选中的`radio`
的样式。同时，为了把不同的`radio`组成一个组，我们需要为同一个组的`radio`指定相同的`name`值。

## 定义主题变量

要定义主题变量，我们只需要在`:root`中定义一个`--form-control-color`就行。如下：

```css
:root {
    --form-control-color: green;
}
```

## 重置`box-sizing`属性

为了在各个平台中表现的一致性和方便计算。我们需要重置一个`box-sizing`属性为`border-box`。如下：

```css
*,
*:before,
*:after {
    box-sizing: border-box;
}
```

## 定义`lable`的样式

由于我们在`label`上使用的class为`form-control`，所以，当我们要为`lable`定义样式的时候，我们需要对`form-control`进行设置。
```css
.form-control {
    font-family: system-ui, sans-serif;
    font-size: 2rem;
    font-weight: bold;
    line-height: 1.1;
    display: grid;
    grid-template-columns: 1em auto;
    gap: 0.5em;
}

.form-control + .form-control {
    margin-top: 1em;
}
```

在这里，我们通过把`display`属性设置为`grid`，来控制`label`中`input`和`text`内容的布局。使其中的`input`的宽度只占用1个字体大小，并且和文字之间保持半个字体的间距。而且在其中的`input`元素也可以改变其大小。如果我们要求两个`radio`元素以水平方式平铺的话，我们需要修改下面两个属性:

```diff
.form-control{
+ display: inline-grid;
- display: grid;
}

.form-control + .form-control {
+ margin-left: 1em;
- margin-top: 1em;
}
```

这样，我们的`lable`的样式就设置成功了。

## 设置`input`样式

在自定义`radio`元素中，设置`input`的样式是重点。

### 去除`input`的本地样式

我们可以使用`appearance`把浏览器默认给`input`加上的特殊样式去除。这样，我们才可以更加方便的为`input`添加样式而不受原有样式的干扰。

```css
input[type="radio"] {
    appearance: none;
    background-color: #fff;
    margin: 0;
}
```

### 为`input`元素添加未选择效果的样式

给`input`元素添加未选择的样式，需要像下面一样：
```css
input[type="radio"] {
    appearance: none;
    background-color: #fff;
    margin: 0;
    font: inherit;
    color: currentColor;
    width: 1.15em;
    height: 1.15em;
    border: 0.15em solid currentColor;
    border-radius: 50%;
    transform: translateY(-0.075em);
}
```
在这里，我们使用到了一个`currentColor`属性值，这个值请参考[基础-颜色](../base/color.md)部分。

在对齐`label`的text和`input`时，我们使用了`transform: translateY`的属性，之所以没有使用`grid`中的`align-items: center`,因为当text过长，最终导致换行时，`input`和文本就无法对齐，而`transform: translate`就可以同时保证单行和多行的对齐。

### 为`input`添加选中样式

先来看代码：
```css
input[type="radio"] {
    /* ...existing styles */
    
    display: grid;
    place-content: center;
}

input[type="radio"]::before {
    content: "";
    width: 0.65em;
    height: 0.65em;
    border-radius: 50%;
    transform: scale(0);
    transition: 120ms transform ease-in-out;
    box-shadow: inset 1em 1em var(--form-control-color);
}

input[type="radio"]:checked::before {
    transform: scale(1);
}
```

我们使用`::bofore`伪元素来为`input`添加选择样式。其中，`height`和`width`选择为合适大小，`border-radius`设置为圆。这里需要注意的2点是：

* 我们使用了`transform:scale(0)`来表示没有选中的状态，然后配合`transtion`可以实现动画，再配置`transform: scale(1)`来显示选择时的效果。
* 我们使用了`box-shadow`而不是`background-color`来显示选中时的颜色，因为确保在打印的时候，可以显示选中状态。

### 高亮对比度和`focus`状态

```css
input[type="radio"]::before {
    /* Window High Contract Mode */
    background-color: CanvasText;
}

input[type="radio"]:focus {
    outline: max(2px, 0.15em) solid currentColor;
    outline-offset: max(2px, 0.15em);
}
```

在这里，我们使用了`CanvasText`来表示在高对比度时的背景色和`outline`属性表示聚焦状态。

## 实验性：使用`:focus-within`来给`label`设置选择状态

```css
.form-control:focus-within {
    color: var(--form-control-color);
}
```

## 完整代码

最后，让我们来看一下完整代码：

html结构
```html
<label class="form-control">
    <input type="radio" name="radio">
    First Radio
</label>

<label class="form-control">
    <input type="radio" name="radio">
    Second Radio
</label>
```

css样式代码：
```css
:root {
    --form-control-color: green;
}

*,
*:before,
*:after {
    box-sizing: border-box;
}

.form-control {
    display: grid;
    grid-template-columns: 1.5em auto;
    gap: 0.5em;
    font-family: monospace;
    font-size: 2rem;
    font-weight: bold;
    line-height: 1.1;
}

.form-control + .form-control {
    margin-top: 1em;
}

.form-control:focus-within {
    color: var(--form-control-color);
}

input[type="radio"] {
    appearance: none;
    background-color: #fff;
    margin: 0;
    font: inherit;
    color: currentColor;
    height: 1.15em;
    width: 1.15em;
    border: 0.15em solid currentColor;
    border-radius: 50%;
    transform: translateY(-0.075em);
    display: grid;
    place-content: center;
}

input[type="radio"]::before {
    content:'';
    width: 0.65em;
    height: 0.65em;
    border-radius: 50%;
    box-shadow: inset 1em 1em var(--form-control-color);
    transform: scale(0);
    transition: transform 120ms ease-in-out;
    background-color: CanvasText;
}

input[type="radio"]:checked::before {
    transform: scale(1);
}

input[type="radio"]:focus {
    outline: max(2px,0.15em) solid currentColor;
    outline-offset: max(2px,0.15em);
}
```
