## flex布局

### 容器的属性

#### 	flex-direction属性

作用:决定主轴的方向(项目的排列方向)

```html
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿
```

#### flex-wrap属性

作用:默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

```html
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}

nowrap（默认）：不换行
wrap：换行，第一行在上方
wrap-reverse：换行，第一行在下方
```



#### flex-flow属性

作用:是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap

```html
.box {
  flex-flow: <flex-direction> <flex-wrap>;
}

```



#### justify-content属性

作用:定义了项目在主轴上的对齐方式

```
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}

flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

```



#### align-items属性

作用:定义了项目在交叉轴上如何对齐

```
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}

flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```



#### align-content属性

作用:定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

```html
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}

flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。
```

### 项目的属性

#### order

​	作用:定义项目的排列顺序,数值越小,排列越靠前

```
.item {
  order: <integer>;
}

```



#### flex-grow

作用:定义项目的放大比例,即如果存在剩余空间,也不放大.

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

```
.item {
  flex-grow: <number>; /* default 0 */
}
```



#### flex-shrink

作用:定义了项目的缩小比例,即如果空间不足,将项目将缩小

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

```
.item {
  flex-shrink: <number>; /* default 1 */
}
```



#### flex-basis

作用:定义了再分配多余空间之前,项目占据的主轴空间(main size), 浏览器根据这个属性,计算主轴是否还有多余空间

```
.item {
  flex-basis: <length> | auto; /* default auto */
}
```



#### flex

作用:是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选

```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```



#### align-self

作用:允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```



## CSS实现动画效果

### transform属性

transform 属性向元素应用 2D 或 3D 转换。该属性允许我们对元素进行**旋转rotate**、**扭曲skew**、**缩放scale**和**移动translate**以及**矩阵变形matrix**

> 语法:
>
> ```css
> transform: none|transform-functions;
> 
> 即：
> transform: rotate | scale | skew | translate |matrix;
> ```
>
> 其中none表示不变换, transfrom-function表示一个或多个变换函数, 以空格隔开



#### 旋转 roate

1. roate(angle): 通过指定的角度参数对原元素指定一个2D旋转

    angle是指旋转角度（单位为deg），如果设置的值为正数表示顺时针旋转，如果设置的值为负数，则表示逆时针旋转。

    

    `transform: rotate(45deg);  `

    

    注意：旋转的时候默认以元素中心点为基点进行旋转，可以通过transform-origin属性定义旋转的基点位置

    **transform-origin属性：定义旋转的基点。**

    语法：

    ```css
    transform-origin: x-axis y-axis z-axis; 
    ```

    默认值：

    ```css
    transform-origin: 50% 50% 0;
    ```

    2D的情况下，默认元素的左上角为0% 0%，例如：绕右下角旋转45度

    ```css
    transform-origin: 100% 100%;
    transform: rotate(45deg);
    ```

2. **rotate3d(x, y, z, angle)**：定义3D旋转

    不常用

3. **rotateX(angle)**：定义沿着X轴的3D旋转

    ```css
    transform: rotateX(45deg);
    ```

4. roateY(angle): 定义沿着Y轴的3D旋转

    ```css
    transform:rotateY(45deg);
    ```

5. **rotateZ(angle)**：定义沿着Z轴的3D旋转

    由以下的例子可以看出，Z轴的方向是垂直于window的方向

    ```css
    transform:rotateZ(45deg);
    ```



#### 移动 translate

1. translate(x, y): 定义2D移动转化

    x 是第一个过渡值参数，y 是第二个过渡值参数选项。如果未被提供，则ty以 0 作为其值。也就是translate(x,y),它表示对象进行平移，按照设定的x,y参数值,当值为负数时，反方向移动物体，其基点默认为元素中心点，也可以根据transform-origin进行改变基点。

    例如：

    ```css
    transform:translate(50px,50px):
    ```

2. translate(x): 指定x轴方向上的一个移动

    ```css
    transform:translateX(50px):
    ```

3. **translate(y)**：指定Y轴方向上的一个移动

    ```css
    transform:translateY(50px):
    ```

4. **translate3d(x, y, z)**：定义3D移动转换

5. **translateZ(z)**：指定Z轴方向上的一个移动



#### 缩放 scale

1. **scale(x, y)**：定义2D缩放转换。

    X表示水平方向缩放的倍数，Y表示垂直方向的缩放倍数，而Y是一个可选参数，如果没有设置Y值，则表示X，Y两个方向的缩放倍数是一样的。并以X为准。例如：

    ```css
    transform: scale(0.7, 0.3);
    ```

    可以通过transform-origin对元素的基点进行设置，同样基点在元素中心位置；例如：

    ```css
    transform-origin: 100% 100%;
    transform: scale(0.7, 0.3);
    ```

2. **scaleX(x)**：在X轴方向进行缩放转换

    ```css
    transform: scaleX(0.7)
    ```

3. **scaleY(y**)：在Y轴方向进行缩放转换

    ```css
    transform: scaleY(0.7)
    ```

4. **scale3d**：(x, y, z)：定义3D缩放转换

5. **scaleZ(z)**：在Z轴方向进行缩放转换



#### 扭曲 skew

1. **skew(x-angle, y-angle)** ：定义沿着 X 和 Y 轴的 2D 倾斜转换。

    skew是用来对元素进行扭曲变行，第一个参数是水平方向扭曲角度，第二个参数是垂直方向扭曲角度。其中第二个参数是可选参数，如果没有设置第二个参数，那么Y轴为0deg。：

    ```css
    transform: skew(10deg,10deg);
    ```

    ![img](https://pic1.zhimg.com/80/v2-2aedd562c5769787542ed7ae34ee19bc_1440w.png)

    同样是以元素中心为基点，我们也可以通过transform-origin来改变元素的基点位置。例如

    ```css
    transform-origin: 100% 100%;
    transform: skew(10deg,10deg);
    ```

    ![img](https://pic3.zhimg.com/80/v2-2cfc4a4eea061c0f2c3e4f4316d8c972_1440w.png)

2. **skewX(angle)**：定义沿着 X 轴的 2D 倾斜转换

    ```css
    transform: skewX(10deg);
    ```

    ![img](https://pic4.zhimg.com/80/v2-8520dcb711395d66105ac236b659a6bf_1440w.png)

3. **skewY(angle)**：定义沿着 Y轴的 2D 倾斜转换

    ```css
    transform: skewY(10deg);
    ```

    ![img](https://pic1.zhimg.com/80/v2-2954448e76799950ad13994fe1310c6c_1440w.png)

    **注意**：如果要实现3D效果，需要将transform-style属性设置为preserve-3d，即

    ```css
    transform-style: preserve-3d;
    ```





### @keyframes

**CSS3中添加的新属性animation是用来为元素实现动画效果的，但是animation无法单独担当起实现动画的效果。承载动画的另一个属性——@keyframes。使用的时候为了兼容可加上-webkit-、-o-、-ms-、-moz-、-khtml-等前缀以适应不同的浏览器**

创建动画的原理是，将一套 CSS 样式逐渐变化为另一套样式。

通过 @keyframes 规则，您能够创建动画。

@keyframes定义一个动画，并定义具体的动画效果，比如是放大还是位移等等。

@keyframes 它定义的动画并不直接执行，需要借助animation来运转。

在动画过程中，您能够多次改变这套 CSS 样式。

以百分比来规定改变发生的时间，或者通过关键词 “from” 和 “to”，等价于 0% 和 100%。

百分比是指动画完成一遍的时间长度的的百分比 ，0% 是动画的开始时间，50%是动画完成一半的时间，100% 动画的结束时间。百分比后面的花括号写：在动画执行过程中的某时间点要完成的变化。

为了获得最佳的浏览器支持，您应该始终定义 0% 和 100% 选择器。

语法:

`@keyframes animationname {keyframes-selector {css-styles;}} `

![在这里插入图片描述](https://img-blog.csdnimg.cn/fe746baca3db4803b09cdb7373a67ea4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAamFja2l5bG9uZw==,size_20,color_FFFFFF,t_70,g_se,x_16)

> 名字为gif的@keyframes ，动画完成需要的总时长为1.4s,刚开始的时候图片旋转为0度，动画完成的时候图片旋转360度

```css
.load-border {
    width: 120px;
    height: 120px;
    background: url(../images/loading_icon.png) no-repeat center center;
    -webkit-animation: gif 1.4s infinite linear;
    animation: gif 1.4s infinite linear; 
}
@keyframes gif {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
        transform: rotate(360deg);
    }
}

```

> 名字为mymove的@keyframes ，动画完成需要的总时长为1s,刚开始的时候图片距顶部距离为0px，0.25s后图片距顶部距离为200px，0.5s后图片距顶部的距离为100px，以此类推

```css
.img {
    width: 120px;
    height: 120px;
    background: url(../images/icon.png) no-repeat center center;
    -webkit-animation: gif 1.4s infinite linear;
    animation: mymove 1s infinite linear;
}
@keyframes mymove
{
    0%   {top:0px;}
    25%  {top:200px;}
    50%  {top:100px;}
    75%  {top:200px;}
    100% {top:0px;}
}

```

> 在一个动画中改变多个 CSS 样式：

```css
@keyframes mymove
{
    0%   {top:0px; background:red; width:100px;}
    100% {top:200px; background:yellow; width:300px;}
}

```



### animation(动画)属性

#### 语法

```
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```



| 值                        | 说明                                                         |
| :------------------------ | :----------------------------------------------------------- |
| animation-name            | 指定要绑定到选择器的关键帧的名称                             |
| animation-duration        | 动画指定需要多少秒或毫秒完成                                 |
| animation-timing-function | 设置动画将如何完成一个周期                                   |
| animation-delay           | 设置动画在启动前的延迟间隔。即是指动画延迟执行时间           |
| animation-iteration-count | 定义动画的播放次数。无限循环关键字 ==infinite==,即是反复循环播放动画 |
| animation-direction       | 指定是否应该轮流反向播放动画。                               |
| animation-fill-mode       | 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。 |
| animation-play-state      | 指定动画是否正在运行或已暂停。                               |
| initial                   | 设置属性为其默认值。                                         |
| inherit                   | 从父元素继承属性。                                           |

##### *animation-timing-function*

规定动画的速度曲线. 默认是"ease"

常见的动画速度参数:

1. linear: 线性过渡. 
2. ease: 平滑过渡
3. ease-in: 由慢到快
4. ease-out: 由快到慢
5. ease-in-out: 由慢到快再到慢
6. step-start: 等同于steps(1, start)
7. step-end: 等同于steps(1, end)
8. steps(<integer>[, [ start | end ] ]?)：接受两个参数的步进函数。第一个参数必须为正整数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点。第二个参数是可选的，默认值为end
9. cubic-bezier(<number>, <number>, <number>, <number>)：特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内

##### *animation-direction*

规定动画是否在下一周期逆向的播放. 默认是"normal"

1. reverse: 反方向运行
2. alternate: 动画先正常运行再反方向运行,并持续交替运行
3. alternate-reverse: 动画先反运行再正方向运行,并持续交替运行

##### *animate-fill-mode*

规定对象动画时间之外的状态

1. none: 默认值, 不设置对象动画之外的状态
2. forwards: 设置对象状态为动画结束时 的状态
3. backwards: 设置对象状态为动画开始时的状态
4. both: 设置对象状态为动画结束或开始的状态, 动画开始之前是"form"或"0%"关键帧; 动画完成之后是"to"或"100%"关键帧状态 

