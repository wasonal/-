### 介绍
Canvas是HTML5新增的组件，它享事一块幕布，可以用js在上面绘制各种图
设置canvas元素的width和height属性指定可以绘图的区域大小
```
//下面的canvas定义了一个指定尺寸的矩形框
<canvas id="test-canvas" width="300" height="200">
    <p>Sorry,your browser don't support canvas</p>
</canvas>
由于浏览器对HTML5标准支持不一致，所以可以在<canvas>内部添加一些说明性的HTML代码，如果支持，则内部的HTML被忽略，否则将显示
```
### 基本使用
#### 2D
**获取绘图对象**
```
var canvas = document.getElementById('test-canvas');
var context = canvas.getContext('2d');//获得CanvasRenderContext2D对象，我们通过这个对象来进行绘图操作
```
**坐标系统**：以左上角为原点，水平向右为x轴，垂直向下为y轴，以像素为单位
### 方法
方法名|参数|描述
:--|:--|:--
toDataURL()|MIME类型|将canvas元素上绘制的图像以MIME的形式导出
strokeRect()|矩形的x坐标，y坐标，矩形的宽度，矩形的高度(均以像素为单位)|绘制只有描边的矩阵
fillRect()|矩形的x坐标，y坐标，矩形的宽度，矩形的高度(均以像素为单位)|绘制实心矩阵
clearRect()|矩形的x坐标，y坐标，矩形的宽度，矩形的高度(均以像素为单位)|清空矩阵内的部分
rect()|矩形的x坐标，y坐标，矩形的宽度，高度|绘制一个路径
beginPath()| |绘制路径前必须调用该方法
arc()|圆心的x坐标，y坐标，radius半径，startAngle起始角度，endAngle结束角度，是否按逆时针计算|绘制圆弧线
lineTo()|结束点x坐标，y坐标|从上一个点开始绘制一条到(x,y)的直线
moveTo()|结束点x坐标，y坐标|将绘图游标移动到(x,y)
fill()| |用fillStyle填充绘制的路径
closePath()| |绘制一条连接点的线
stroke()| |用strokeStyle对路径描边
clip()| |在路径上创建一个剪切区域
### 图像处理

### 属性
属性名|可选值|描述
:--|:--|:--
fillStyle|颜色|填充颜色，默认为#000
strokeStyle|颜色|描边颜色，默认为#000

### 注意点
**宽高设置**   
方法1：<canvas width="500" height="500"></canvas>   
方法2：
```
var canvas = document.getElementById("canvas");
canvas.width = 500;canvas.height = 500;
```
但是如果仅通过style中的width和height的话（错误）就会引起绘制部分的拉伸，因为canvas的画布默认是width:150px,height:300px;而在style中设置的height,width是canvas在DOM中占位的大小，所以在设置错误的情况下，canvas会对绘制部分进行拉伸
**显示顺序**
后来者居上

Canvas状态是以栈的方式来保存：每次调用save()方法，就会把当前状态压入栈顶保存；每次调用restore()方法，就会把栈顶的状态取出来，并把画布恢复到这个状态，用这个状态绘图

rotate()，scale()都会影响画布

### 实战
实现图片裁剪   
获取页面大小
数据转换
```
// 获取包含图片信息的 data URI
let data = canvas.toDataURL(); 
// data URIs 的语法结构为：data:[<mediatype>][;base64],<data>     我们只需要 <data> 部分
data = data.spilt(',')[1];
// 解码base-64编码的数据
data = window.atob(data);
// 无符号整型数组
const u = new Uint8Array(data.length);
// 转化为 Unicode 值
for (var i = 0; i < data.length; i++) {
    u[i] = data.charCodeAt(i);
}
// 构建 Blob 类文件对象
const blob = new Blob([u], { type: "image/png" })
```
https://blog.csdn.net/qq_38702697/article/details/83689001