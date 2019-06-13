### transition
#### 介绍
transition能够更改CSS属性变化时的速度，让其变化称为一个持续一段时间的过程而不是立即生效。   
transition:设置过渡效果的css属性名称 过渡效果的时间 过渡效果速度曲线 过渡效果开始的延迟时间/秒;   
属性名|描述|属性值
:--|:--|:--
transition-property|指定用于过渡的CSS属性|
transition-duration|指定动画过渡的事件/(s,ms)，默认值为0不会有效果|
transition-time-function|过渡效果速度曲线|ease慢快慢、linear匀速、step-end、steps(n,end)
transition-delay|过渡效果开始的延迟时间/(s,ms)|
#### 注意点
> 以transition-property的值列表长度为标准，其他属性过长则截短，过短则重复
> 设置多个属性的时候用','隔开
> 不是所有的属性都支持transition
> transition的开始状态和结束状态都需要具体数值，否则不会产生动画效果
#### 过渡事件
当**过渡完成**时触发一个事件，标准事件是transitionend，WebKit下是webkitTransitionEnd   
transitionend事件主要有两个属性
propertyName: (字符串)指示已完成过渡的属性
elapsedTime：(浮点数)指示当触发这个事件时过渡已运行的事件
#### 局限性
> 需要事件触发
> transition是一次性的不能重复发生，需要重新触发
> transition只能定义开始状态和结束状态不能定义中间状态
> 一条transition规则只能定义一个属性的变化
animation则是为了解决以上这些问题才提出的
### @keyframes关键帧规则
#### 介绍
@keyframes规则通过在动画序列中定义关键帧的样式来控制CSS动画序列中的中间步骤，需要配置动画序列使用，举个例子：
```
@-webkit-keyframes slidein{
    from{
        margin-left: 100%;
        width: 300%;
    }
    to{
        margin-left: 0%;
        width: 100%;
    }
}
```
其中**slidein**是这个规则的名字，后续可使用animation-name来将一个动画和它的关键帧作匹配。   
另外也可以用百分比值来命名关键帧
#### 注意点
1. 关键帧规则没有指定动画开始或结束状态，浏览器将使用元素现有状态作为起始/结束状态
2. 关键帧中不能用作动画的属性会被忽略掉
3. 重复定义的关键帧百分比，同名关键帧都以最后一次定义的为准
4. 关键帧中的!important会被忽略掉
### animation
#### 介绍
animation和@keyframes创建动画序列，该属性允许配置动画时间、时长以及其他细节，但不能配置动画的实际表现，动画的实际表现由@keyframes规则实现   
animation: 绑定的关键帧名字 动画时间/秒 动画速度曲线 动画开始时的延迟/秒 动画播放次数 动画播放方向 动画执行前后的目标样式 动画是否运行和暂停;   
属性名|描述|属性值
:--|:--|:--
animation-name|绑定的关键帧名字|如上面的关键帧规则中的slidein
animation-duration|动画时间/(s,ms)|
animation-function|动画速度曲线|linear匀速、ease慢快慢、ease-in慢快、ease-out快慢、ease-in-out慢快慢、cubic-bezier(n,n,n,n)自定义函数
animation-delay|动画开始时的延迟/(s,ms)|
animation-iteration-count|动画播放次数|n播放n次、infinite播放无限次
animation-direction|动画播放方向|normal正常播放、alternate正反向轮流播放
animation-fill-mode|动画执行前后的目标样式|none动画执行前后不改变样式、forwards保持最后一帧的样式、backwards保持第一帧的样式、both设置forwards和backwards
animation-direction|动画是否暂停或运行|paused停止动画、running运行动画
#### 注意
父元素的display属性none和其他属性切换触发amination

#### 动画事件AnimationEvent
animationstart| animationend| animationiteration



### transform
#### 介绍
transform属性允许我们对**块级元素**进行旋转、缩放、倾斜   
transform:transform-function
function-name|描述
:--|:--
rotate(n deg)|顺时针旋转n度
translate(x,y)|在平面上移动元素坐标x,y个单位，如果是百分比则以元素本身为基准，translate(2)等于translate(2,2)
translateX(x)|在平面上水平移动元素坐标x个单位
translateY(y)|在平面上垂直移动元素坐标y个单位
scale(x,y)|以元素中心点缩放，缩放基数为1，大于1放大，小于1缩小，为赋值的时候就会对元素进行翻转
scaleX(x)|x轴方向缩放
scaleX(y)|y轴方向缩放
skew(x,y)|x轴和y轴按照一定角度值进行扭曲变换
matrix(a,b,c,d,e,f)|
#### transform-origin
设置旋转元素的基点位置
transform-origin: x-axis y-axis z-axis;   
属性|描述
:--|:--
x-axis|基点的x坐标(默认50%)
y-axis|基点的y坐标(默认50%)
z-axis|基点的z坐标(默认0)
#### 与amination的共同使用
transform会失效
参考链接：[CSS3动画理解与应用](https://www.cnblogs.com/jingwhale/p/4641385.html)   
[CSS3中的变形](https://www.cnblogs.com/starof/p/4560076.html)