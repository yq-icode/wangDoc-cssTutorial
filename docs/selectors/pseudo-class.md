# 伪类选择器

伪元素（pseudo-element）是 HTML 中并不存在的元素。例如，定义第一个字母或第一行文字时，并未在HTML中作相应的标记。

伪类（pseudo-class）则应用于一组 HTML 元素，而你无需在 HTML 代码中用类标记它们。例如，使用:first-child可以选择某元素的第一个子元素，你就不用写成class="first-child"。更多关于伪类的内容。

伪元素有四个。

- ::first-line
- ::first-letter
- ::before
- ::after

伪类

- :first-child
- :link：新的、未访问的链接
- :visited：访问过的链接
- :focus：链接获得焦点（如通过Tab键）
- :hover：当访问者将鼠标指针停留在链接上时
- :active: 当访问者激活链接时

新的、未访问的链接显示为红色；访问过的链接变为橙色；



## 概述

CSS 2.1非常有限，只提供了三个伪类。

- :active
- :focus
- :hover

CSS Selector Level 3添加了更多与HTML表单相关的伪类：

- :enabled
- :disabled
- :checked
- :indeterminate

CSS Basic UI Level 3添加了许多伪类来描述窗口小部件的状态：

- :default
- :valid
- :invalid
- :in-range
- :out-of-range
- :required
- :optional
- :read-only
- :read-write

## :first-child，:last-child

`:first-child`表示一组元素的第一个元素，且该元素必须是父元素的第一个子元素。

```css
li{
  color: blue;
}

li:first-child {
  color: green;
}
```

上面代码中，第一个`li`的字体颜色为绿色，其他`li`都为蓝色。

`:last-child`表示一组元素之中的最后一个，且该元素必须是父元素的最后一个子元素。

```css
li:last-child {
  background-color: lime;
}
```

## :first-of-type，:last-of-type

`:first-of-type`选中一组元素之中的第一个元素。

```css
p:first-of-type {
  font-size: 1.25em;
}
```

上面代码中，`p:first-of-type`只会选中第一个`p`元素。

`:first-of-type`与`:first-child`的区别是，后者必须父元素的第一个子元素。

```html
<ul>
  <p>Hello World</p>
  <li>1</li>
  <li>2</li>
</ul>
```

上面这段 HTML 代码，如果想让第一个`<li>`显示为绿色，必须使用`:first-of-type`，而不能是`:first-child`。

```css
/* 正确 */
ul li:first-of-type {
  color: green;
}

/* 错误 */
ul li:first-child {
  color: green;
}
```

`:last-of-type`选中本类之中最后一个元素。

```css
p:last-of-type {
  font-size: 0.75em;
}
```

上面代码中，`p:last-of-type`只会选中最后一个`p`元素。

## :nth-child()，:nth-last-child()

`:nth-child()`选中本类之中指定位置的元素。`:nth-last-child()`选中本类之中指定的倒数位置的元素。

```css
p:nth-child(2) {
  color: red;
}
```

上面代码中，`:nth-child()`选中第二个`p`元素。

`:nth-child()`和`:nth-last-child()`可以使用通配符作为参数，参见`:nth-of-type()`部分的说明。

```css
ul li:nth-child(3n+3) {
  color: #ccc;
}
```

上面代码选中3、6、9等位置的`li`元素，`n`表示整数序列0、1、2、3……。

这里还有一个技巧，如果要选中前三个元素，可以在`n`前面使用负数符号`-`。

```css
ul li:nth-child(-n+3) {
  color: #ccc;
}
```

上面代码只会选中前三个`li`，因为当`n`大于等于`3`时，`-n+3`会小于等于0，而`li`的序号是从`1`开始的。

相应的，`:nth-last-child(-n + 3)`就会选中最后三个元素，而`:nth-last-child(n + 4)`会选中除了最后三个以外的其他元素。

除了使用`an+b`这种形式的表达式指定位置，还可以使用`odd`或`even`关键字，分别表示奇数位置或偶数位置的元素。

```css
ul li:nth-child(odd) {
  color: #ccc;
}
```

## :nth-of-type()，:nth-last-of-type()

`:nth-of-type()`选中指定类型和指定位置的元素，`:nth-last-of-type()`选中倒数位置的指定类型和指定位置的元素。

```css
p:nth-of-type(2) {
  color: red;
}
```

`:nth-of-type`选中子元素之中的第二个`p`元素。

通配符用法。

```css
li:nth-of-type(2n) {
  background: lightslategrey;
}

li:nth-of-type(3n+2) {
  background: blue;
}
```

`:nth-of-type`的参数可以是`an + b`的形式。

- “a”是一个整数
- “n”作为英文字母，总是不变的，含义是“0, 1, 2, ....”
- “+”作为一个运算符，可以是“+”，也可以是“-”
- “b”是一个整数，如果提供了运算符，就必须提供“b”

`:nth-of-type`的参数还可以是`even`或`odd`。

```css
li::nth-of-type(odd)  {
  background: lightslategrey;
}
```

