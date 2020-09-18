# animation
- 使用简写属性，将动画与 div 元素绑定

## 语法 
|animation|name|duration|timing-function|delay|iteration-count|direction|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|默认值|none|0|ease|0|1|normal|
|解释| @keyframe的名称|动画总时间(秒、毫秒)|动画速度曲线|动画开始前的等待时间|播放次数|规定是否应该轮流反向播放动画|
|注意| -- |0就是不播放动画|--|允许负值，-2s使动画马上开始，但跳过2秒进入动画周期|infinite-循环播放|alternate - 正常播放后再反向播放|

### timing-function - [测试地址 ](https://www.w3school.com.cn/tiy/t.asp?f=css3_animation-timing-function2)
|value|描述|cubic-bezier|
|:---:|:---:|:---:|
|linear|匀速|cubic-bezier(0,0,1,1)|
|ease|以低速开始，然后加快，在结束前变慢|cubic-bezier(0.25,0.1,0.25,1)|
|ease-in|以低速开始|cubic-bezier(0.42,0,1,1)|
|ease-out|以低速结束|cubic-bezier(0,0,0.58,1)|
|ease-in-out|以低速开始和结束|cubic-bezier(0.42,0,0.58,1)|

#### cubic-bezier() - 贝塞尔曲线(Cubic Bezier)
- 贝塞尔曲线曲线由四个点 P0，P1，P2 和 P3 定义. P0 和 P3 是曲线的起点和终点.

## JS赋值语法
|内容|key|value|
|:---:|:---:|:---:|
|animation|object.style.animation|mymove 5s infinite|
|animation-name|object.style.animationName|mymove|
|animation-duration|object.style.animationDuration|3s|
|animation-timing-function|object.style.animationTimingFunction|linear|
|animation-delay|object.style.animationDelay|2s|
|animation-iteration-count|object.style.animationIterationCount|3|
|animation-direction|object.style.animationDirection|alternate|
