# CSS笔记
## CSS的背景

### 背景颜色
```css
background-color:transparent(透明);
```

### 背景图片
```CSS
background-image:url(图片地址)
```

### 背景平铺
```css
background-repeat:no-repeat\repeat\repeat-y\repeat-x
```

### 背景图片的位置
```css
background-position:x y;
```
x，y可以是**方位名词**或**精确单位**    
|  参数值  |                   说明                   |
| :------: | :--------------------------------------: |
|  length  |                  百分数                  |
| position | top\right\left\bottom\center各种方位名词 |
##### 参数是方位名词
1.x，y两个参数位置顺序可以调换，效果一样。
```css
background-position:center right;
```
```css
background-position:right center;
```
2.当x，y省略其中一个参数时，省略的参数默认为center。
```css
background-position:right;
```
- 此时为水平靠右，垂直居中。
##### 参数是精确单位
- 如果参数是精确单位，第一个一定是x坐标，第二个一定是y坐标，参数有严格的顺序。
- 如果省略一个参数，那么剩下的那个参数一定是x的，那么y就为center.
##### 参数是混合单位
- 特点和参数是精确单位时一样，x，y有严格的顺序。

### 使背景图片充满设定区域
```css
/* 这个写法会自动适应浏览器大小 */
background-size:100% 100%;
/* 或者 */
background-size:cover;
```

### 背景图像固定(视差滚动)
```css
background-attachment:scroll | fixed
```
| 参数   |             作用             |
| :----- | :--------------------------: |
| scroll | 背景图像是随着对象的内容移动 |
| fixed  | 背景图像固定住，不随内容移动 |

### 背景色半透明
```css
background:rgba(0,0,0,0.3);
```
- 最后一个参数就是alpha透明度，取值在0~1间
- 实际开发中，我们习惯把它写成`background:rgba(-,-,-,.3);`
- 主要：背景半透明是指盒子背景半透明，盒子里面的内容不受影响

### 背景总结
| 属性                  | 作用           | 值                                                                 |
| :-------------------- | :------------- | :----------------------------------------------------------------- |
| background-color      | 背景颜色       | 预定义的颜色单词/十六进制/RGB代码                                  |
| background-image      | 背景图片       | url(图片路径)                                                      |
| background-repeat     | 背景平铺       | no-repeat(不平铺)/repeat(平铺)/repeat-x(x轴平铺)/repeat-y(y轴平铺) |
| background-position   | 背景位置       | length/position 分别是x和y坐标                                     |
| background-attachment | 背景固定       | scroll(背景移动)/fixed(背景固定)                                   |
| 背景简写              | 书写更加简单   | 顺序：背景颜色 背景图片地址 背景平铺 背景滚动 背景位置             |
| 背景色半透明          | 背景颜色半透明 | background:rgba(-,-,-,.3);后面必须是4个值                          |
---
## CSS三个特性
### CSS层叠性
主要解决当给同一个选择器设置相同的样式时，样式冲突的问题。
层叠性原则：
- 样式冲突，先设置的那个样式会被后面设置的样式覆盖掉
- 给同一个选择器设置的样式不一样，不会覆盖

### 继承性
父标签的一些样式会被子标签继承( **text-,font-,line-** 这些元素开头的可以继承，以及 **color** 属性)
```css
<div>
    <p>
    </p>
</div>
```
上面的p标签会继承div标签的一些样式。
##### 行高的继承
```css
/* 1.5表示的是当前行高是当前文字大小 font-size 的1.5倍 */
body {
    font:12px/1.5 Microsoft YaHei;
}
```
- 行高可以跟单位也可以不跟单位
- 这种写法的优势是可以让子元素根据自己的文字大小自动调整行高

### 优先级(权重)
| 选择器               | 权重值 |
| :------------------- | :----- |
| 继承或者*            | 0      |
| 元素选择器           | 1      |
| 类选择器，伪类选择器 | 10     |
| id选择器             | 100    |
| 行内样式 style=""    | 1000   |
| !important重要的     | 无穷大 |
---
## 盒子模型
页面布局学习三大核心盒子模型、浮动、定位。
### 边框(border)
```css
border:border-width(边框粗细)||border-style(一般为solid<实线>/dashed<虚线边框>/dotted<点线边框>)||border-color(边框的颜色)
```
##### 边框分开设置样式
border-需要设置的那条边的单词
```css
border-top:10px solid red;
```
##### 表格的细线边框
border-collapse属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框
语法：
```css
border-collapse:collapse;
```
- collapse单词是合并的意思
- border-collapse:collapse;表示相邻边框合并在一起

### 内边距(padding)
内容和边框之间的距离。
语法：
```css
padding:10px；
```
当padding跟不同个数的值，代表不同的情况：
- 一个值，四个内边距一样
- 两个值，上下内边距一样5px，左右内边距一样10px
padding:5px 10px;
- 三个值，上内边距一个值5px，左右内边距一样10px，下内边距一个值20px
padding：5px 10px 20px;
- 四个值，按顺时针设置赋值。
padding:5px 10px 20px 30px;
需要注意的是：当盒子有了内边距后，盒子的大小发生了改变，这时就需要将原来盒子的大小减去内边距的大小，这样才能得到原来需要盒子的大小。
比如：需要一个200X200大小的盒子，内边距设置是20px，则需要width-40px，height-40px，才会的到一个200X200的盒子。
**在实际开发中，当导航栏中的字数不同时，可以使用padding撑开盒子使得每个栏目的距离相同**

### 外边距(margin)
```css
margin:30px;
```
用法和padding基本一样。
#####外边距典型应用
外边距可以让块级盒子**水平居中**，但需要满足两个条件：
- 盒子必须指定了宽度(width)
- 盒子**左右的边距**都设置为auto
```css
.header {
    width:960px;
    margin:0 auto;
}
```
##### 外边距合并
1.相邻块元素垂直外边距的合并
- 设置两个相邻盒子垂直方向的外边距，会取两者中数值大的。解决方案就是只给一个盒子添加margin值。

2.嵌套块元素垂直外边距的塌陷
- 对于嵌套的块元素(父子块元素)，父元素有上边距同时子元素也有上边距，此时父元素会塌陷较大的外边距值。解决方案：①给父元素定义一个1px的边框，②给父元素定义一个1px的内边距，③给父元素添加语句：`overflow:hidden`
- 还有其他方法，比如浮动，固定，绝对定位的盒子不会有塌陷问题。

### 清除网页默认的内外边距
```css
* {
    padding:0;
    margin:0;
}
```
注意：行内元素尽量只设置左右的内外边距，不要设置上下内外边距。当然也可以转换成块元素和行内块元素后再设置。

## 圆角边框(重点)
```css
/* length(相当于圆的半径半径)越大，弧度越大
可以用精确单位，也可以用百分比 */
border-radius:length;

/* 圆形的做法 */
/* 先设置一个正方形的盒子，将length设置为盒子height的一半 */
width:200px;
height:200px;
border-radius:100px/50%;

/* 圆角矩形的做法 */
/* 直接将length设置为矩形盒子height的一半 */
width:200px;
height:100px;
border-radius:50%;

/* 对于不同弧度的圆角设置 */
width:200px;
height:100px;
/* 分别表示上左、上右、下右、下左，延顺时针赋值 */
border-radius:10px 20px 30px 40px;
/* 若只设置两个参数，那么对角线弧度相同 */
/* 上左和下右一样，上右和下左一样 */
border-radius:10px 20px;
/* 若设置三个参数，那么第一个代表上左，第三个代表下右，第二个代表上右和下左 */
border-radius:10px 20px 30px;
/* 若只需要设置一个圆角 */
/* 必须先写上下，再写左右 */
border-top-left-radius:10px;
```

## 盒子阴影(重点)
| 值       | 描述                                               |
| :------- | :------------------------------------------------- |
| h-shadow | 必需。水平阴影的位置，允许负值                     |
| v-shadow | 必需。垂直阴影的位置，允许负值                     |
| blur     | 可选。阴影的虚实程度，0为最实，越大越模糊          |
| spread   | 可选。阴影的大小                                   |
| color    | 可选。阴影的颜色，一般使用**rgba**                 |
| inset    | 可选。将外部阴影(outset)改为内部阴影，默认为outset |
```css
box-shadow:h-shadow v-shadow blur spread color inset;
/* 当鼠标经过盒子时产生阴影 */
div:hover {
    box-shadow:h-shadow v-shadow blur spread color inset;
}
```

## 文字阴影
```css
text-shadow:h-shadow v-shadow blur color;
/* 参数描述和box-shadow一样 */
```

## 浮动(重点)
### 标准流
标准流：标签按照规定好默认方式排列。
**网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。**

### 浮动原理(float)
```css
选择器{float:属性值}
```
float属性用于创建浮动框，将其移动到所要求属性的一边，直到触及该边包含块或另一个浮动框的边缘。**浮动后的元素不占用其原来的空间。**

### 浮动特性(重点)
- 浮动元素会脱离标准流，并移动到指定的位置
- 浮动的元素会以行内显示并且元素顶部对齐
- 当父级盒子装不下过多的盒子，多出的盒子会另起一行对齐
- 浮动的元素会具有**行内块元素**的特性(可以给行内元素或块级元素添加浮动，使其具有行内块元素的特点)
- 浮动的盒子不再保留原先的位置
- 如果块级盒子没有设置宽度，默认宽度和父级一样宽，但是添加浮动后，它的宽度根据内容来决定

### 清除浮动
在开发中，我们经常需要设置父盒子包含子盒子，这时父盒子往往不合适给高度(因为有时需要装很多的子盒子，不清楚高度需要给多少)，这时就希望子盒子能够自动撑开父盒子，但是当子盒子浮动后，会使父盒子的高度变为0(盒子浮动后不占位置)，父盒子下面的盒子就会升上来占用其原来的位置。
##### 清除浮动的本质
- 清除浮动就是清除浮动的元素造成的影响
- 如果父盒子本身有高度，则不需要清除浮动
- 清除浮动后，父级就会根据浮动的子盒子自动检测高度，父级有了高度，就不会影响下面的标准流
##### 语法
```css
/* 方法一：在最后一个子盒子后面添加一个块级元素标签，再对该标签赋予样式 */
选择器 {clear: both/left/right}

/* 方法二：父级添加overflow属性 */
overflow: hidden;

/* 方法三：给父级添加:after伪元素 */
.clearfix:after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix {
    /* IE6、7专有 */
    *zoom: 1;
}

/* 方法四：给父元素添加双伪元素 */
.clearfix:before,
.clearfix:after {
    content: "";
    display: table;
}
.clearfix:after {
    clear: both;
}
.clearfix {
    *zoom: 1;
}
```

## 定位
### 定位组成
定位：将盒子定在某一个位置，所以定位也是在摆放盒子，按照定位的方式移动盒子。
定位 = 定位模式 + 边偏移
**定位模式**用于指定一个元素在文档中的定位方式。**边偏移**决定该元素的最终位置。
##### 定位模式
定位模式决定元素的定位方式，通过position属性进行设置，一共有四种定位方式：
- position：static 默认值，没有定位，元素出现在正常流中
- position：fixed 固定定位，相对于浏览器可视窗口来进行定位
- position：relative 相对定位，相对于其本身正常位置来进行定位，它原本所占的空间仍保留
- position：absolute 绝对定位，相对于定位方式不是static的第一个祖先元素进行定位
