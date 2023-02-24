# 自定义CheckBox按钮

自定义CheckBox按钮的方法在大体上和[自定义Radio按钮](./radio.md)
的方法是一样的。其中相同的部分就不再这里那赘述了。请参考[自定义Radio按钮](./radio.md)。

## 整体代码

html部分

```html
<label class="form-control">
    <input type="checkbox" name="checkbox"/>
    Checkbox
</label>

<label class="form-control">
    <input type="checkbox" name="checkbox-checked"/>
    Checkbox Checked
</label>

<label class="form-control form-control--disabled">
    <input type="checkbox" name="checkbox-disabled"/>
    Checkbox Disabled
</label>

<label class="form-control form-control--disabled">
    <input type="checkbox" name="checkbox-disabled-checked">
    Checkbox Disabled Checked
</label>
```

css样式部分

```css
:root {
    --form-control-color: green;
    --form-control-disable: grey;
}

*,
*:before,
*:after {
    box-sizing: border-box;
}

.form-control {
    display: grid;
    grid-template-columns: 1em auto;
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

.form-control--disabled {
    color: var(--form-control-disable);
    cursor: not-allowed;
}

input[type="checkbox"] {
    appearance: none;
    background-color: #fff;
    margin: 0;

    width: 1.15em;
    height: 1.15em;

    font: initial;
    color: currentColor;
    border-radius: 4px;
    border: 0.15em solid currentColor;

    display: grid;
    place-content: center;
    transform: translateY(-0.075em);
}

input[type="checkbox"]::before {
    content: '';
    width: 0.65em;
    height: 0.65em;
    clip-path: polygon(14% 44%, 0 65%, 50% 100%,100% 16%, 80% 0%,43% 62%);
    transform: scale(0);
    transform-origin: bottom left;
    transition: transform 120ms ease-in-out;
    box-shadow: inset 1em 1em var(--form-control-color);
    background-color: CanvasText;
}

input[type="checkbox"]:checked::before {
    transform: scale(1);
}

input[type="checkbox"]:focus {
    outline: max(2px,0.15em) solid currentColor;
    outline-offset: max(2px,0.15em);
}

input[type="checkbox"]:disabled {
    --form-control-color: var(--form-control-disabled);
    color: var(--form-control-disabled);
    cursor: not-allowed;
}
```

## 和`Radio`中主要的不同

自定义`Checkbox`按钮和自定义`Radio`按钮的主要不同之处在于，选择状态时的样式和添加了一个`disabled`状态样式。

[//]: # (todo: 添加和`Radio`中的不同部分)
