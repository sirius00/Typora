# Scss的基本用法

## 声明变量

声明变量的符号 $

```css
$color: #333;
.a {
color: $color;
}
```

## 默认变量 (!default)

scss的默认变量仅需要在值后面加上!default即可

```css
$color: #333 !default;
.a {
color: $color;
}
```

如果分配给变量的值后面添加了 !default 标志 ，这意味着该变量如果已经赋值，那么它不会被重新赋值，但是，如果它尚未赋值，那么它会被赋予新的给定值

## 变量调用

直接调用即可, 变量声明也可以直接调用已声明的变量

```css
$color: #666;
$color2: $color;
.b {
	color: $color2;
}
```

## 局部变量和全局变量

在元素内部定义的变量不会影响其他元素

```css
em {
  $color: red;  //定义局部变量
  a {
    color: $color; //调用局部变量
  }
}

```



## 嵌套

### 选择器嵌套

结构

```html
<header>
<nav>
    <a href=“##”>Home</a>
    <a href=“##”>About</a>
    <a href=“##”>Blog</a>
</nav>
<header>
```

scss实现

```css
nav {
  a {
    color: red;

    header & {
      color:green;
    }
  }  
}
```



### 属性嵌套

Sass 中还提供属性嵌套，CSS 有一些属性前缀相同，只是后缀不一样，比如：border-top/border-right，与这个类似的还有 margin、padding、font 等属性。

样式如下:

```css
.box {
    border-top: 1px solid red;
    border-bottom: 1px solid green;
}
```



sass实现

```css
.box {
  border: {
   top: 1px solid red;
   bottom: 1px solid green;
  }
}
```



### 伪类嵌套

借助 &

```css
span {
	color:red;
	&:hover {
		color : green;
	}
}
```



## 混合宏

如果你的整个网站中有几处小样式类似，比如颜色，字体等，在 Sass 可以使用变量来统一处理，那么这种选择还是不错的。但当你的样式变得越来越复杂，需要重复使用大段的样式时，使用变量就无法达到我们目了。这个时候 Sass 中的混合宏就会变得非常有意义

### 声明

#### 不带参数混合宏

在sass中, 使用"@mixin" 来声明一个混合宏,如:

```css
@mixin border-radius{
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```

其中 @mixin 是用来声明混合宏的关键词，有点类似 CSS 中的 @media、@font-face 一样。border-radius 是混合宏的名称。大括号里面是复用的样式代码。



#### 带参数混合宏

除了声明一个不带参数的混合宏之外，还可以在定义混合宏时带有参数，如：

```css
@mixin border-radius($radius:5px){
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```



### 调用

在 Sass 中通过 @mixin 关键词声明了一个混合宏，那么在实际调用中，其匹配了一个关键词“ @include ”来调用声明好的混合宏。例如在你的样式中定义了一个圆角的混合宏“border-radius”:

```css
@mixin border-radius{
    -webkit-border-radius: 3px;
    border-radius: 3px;
}

```



在一个按钮中要调用定义好的混合宏“border-radius”，可以这样使用：

```css
button {
    @include border-radius;
}

```



### 混合宏的参数

Sass 的混合宏有一个强大的功能，可以传参，那么在 Sass 中传参主要有以下几种情形：

#### 传一个不带值的参数

在混合宏中，可以传一个不带任何值的参数，比如：

```css
@mixin border-radius($radius){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}

```

在混合宏“border-radius”中定义了一个不带任何值的参数“$radius”。

在调用的时候可以给这个混合宏传一个参数值：

```css
.box {
  @include border-radius(3px);
}
```



#### 传一个带值的参数

在 Sass 的混合宏中，还可以给混合宏的参数传一个默认值，例如：

```css
@mixin border-radius($radius:3px){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```

在混合宏“border-radius”传了一个参数“$radius”，而且给这个参数赋予了一个默认值“3px”。

在调用类似这样的混合宏时，会多有一个机会，假设你的页面中的圆角很多地方都是“3px”的圆角，那么这个时候只需要调用默认的混合宏“border-radius”:

```css
.btn {
  @include border-radius;
}
```



### 混合宏的不足

混合宏在实际编码中给我们带来很多方便之处，特别是对于复用重复代码块。但其最大的不足之处是会生成冗余的代码块。比如在不同的地方调用一个相同的混合宏时。如：

```css
@mixin border-radius{
  -webkit-border-radius: 3px;
  border-radius: 3px;
}

.box {
  @include border-radius;
  margin-bottom: 5px;
}

.btn {
  @include border-radius;
}
```

## 扩展/继承

在 Sass 中是通过关键词 “@extend”来继承已存在的类样式块，从而实现代码的继承。如下所示：

```css
// SCSS
.btn {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}

.btn-primary {
  background-color: #f36;
  color: #fff;
  @extend .btn;
}

.btn-second {
  background-color: orange;
  color: #fff;
  @extend .btn;
}
```

## 占位符 % placeholder

它可以取代以前 CSS 中的基类造成的代码冗余的情形。因为 %placeholder 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。来看一个演示：

```css
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}
```



这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

```css
// SCSS
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}

.btn {
  @extend %mt5;
  @extend %pt5;
}

.block {
  @extend %mt5;

  span {
    @extend %pt5;
  }
}


```