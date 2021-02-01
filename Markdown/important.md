# CSS中常见的属性

- <a href="#boxShadow">box-shadow</a> : 向 div 元素添加阴影

- <a href="#objectFit">object-fit</a> : 指定元素的内容应该如何去适应指定容器的高度与宽度

- <a href="#objectPosition">object-position</a> : 根据容器大小重置图片的大小，并设置图片的位置

## <a name="boxShadow">box-shadow</a> : 向 div 元素添加阴影
- [测试地址](https://www.css88.com/tool/css3Preview/Box-Shadow.html)

### 语法

|box-shadow|h-shadow|v-shadow|blur|spread|color|inset|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|解释| 水平阴影的位置。允许负值 |垂直阴影的位置。允许负值|模糊距离(阴影的模糊度)|阴影的尺寸(阴影的扩展半径)|阴影的颜色|将外部阴影 (outset) 改为内部阴影|
|注意|必需:负左正右|必需:负上正下|可选|可选|可选|可选|

### 例子
```css
div { 
	box-shadow: 1px 2px 3px 4px color inset;
}

div {
    box-shadow:
        /* 内上 */
        inset 0 5px red,
        /* 内下 */
        inset 0 -5px green,
        /* 内左 */
        inset 5px 0 pink,
        /* 内右 */
        inset -5px 0 gray,
        /* 外下 */
        0 5px red,
        /* 外上 */
        0 -5px green,
        /* 外右 */
        5px 0 pink,
        /* 外左 */
        -5px 0 gray;
}
```

###  JS赋值语法
```js
object.style.boxShadow="10px 10px 5px #888888"
```

## <a name="objectFit">object-fit</a> : 指定元素的内容应该如何去适应指定容器的高度与宽度

- object-fit 一般用于 img 和 video 标签，一般可以对这些元素进行保留原始比例的剪切、缩放或者直接进行拉伸等。
- [测试地址](https://www.runoob.com/try/try.php?filename=trycss3_object-fit)

### 语法
|value|描述|
|:---:|:---:|
|fill|默认，不保证保持原有的比例，内容拉伸填充整个内容容器。|
|contain|保持原有尺寸比例。内容被缩放。|
|cover|保持原有尺寸比例。但部分内容可能被剪切。|
|none|保留原有元素内容的长度和宽度，也就是说内容不会被重置。|
|scale-down|保持原有尺寸比例。内容的尺寸与 none 或 contain 中的一个相同，取决于它们两个之间谁得到的对象尺寸会更小一些|
|initial|设置为默认值|
|inherit|从该元素的父元素继承属性|

## <a name="objectPosition">object-position</a> : 根据容器大小重置图片的大小，并设置图片的位置

- [测试地址](https://www.runoob.com/try/try.php?filename=trycss3_object-position)

### 语法
|value|描述|
|:---:|:---|
|position|指定 image 或 video 在容器中的位置。第一个值为 x 坐标位置的值，第二个值为 y 坐标位置的值。表示的方式有<br>object-position: 50% 50%; <br>object-position: right top; <br/>object-position: left bottom; <br/>object-position: 250px 125px;|
|initial|设置为默认值|
|inherit|从该元素的父元素继承属性|

# 关键字

## initial(值) : 用于设置 CSS 属性为它的默认值,可用于任何 HTML 元素上的任何 CSS 属性

