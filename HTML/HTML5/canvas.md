### 介绍
Canvas是HTML5新增的组件，它享事一块幕布，可以用js在上面绘制各种图
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
canvas.getContext('2d');//获得CanvasRenderContext2D对象，我们通过这个对象来进行绘图操作
```
**坐标系统**：以左上角为原点，水平向右为x轴，垂直向下为y轴，以像素为单位

