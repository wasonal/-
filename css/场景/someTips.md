### 多个display:inline/inline-block;标签分行写的时候，显示出来图片之间有间隔
```
<img src="/i/eg_tulip.jpg"  alt="郁金香" height="100px"/>
<img src="/i/eg_tulip.jpg"  alt="郁金香" height="100px"/>
```
**原因**：浏览器把img标签之间的空白当成了空白节点
### 解决方法
1、将img写成并排形式
```
<img src="/i/eg_tulip.jpg"  alt="郁金香" height="100px"/><img src="/i/eg_tulip.jpg"  alt="郁金香" height="100px"/>
```
2、设置img标签的父级font-size:0;
3、设置img标签display:block;float:left;

### 设置input标签placeholder字体的颜色
::-webkit-input-placeholder，:-moz-placeholder， ::-moz-placeholder， :-ms-input-placeholder{
    color: #fff;
}

### IE11 浏览器，元素背景，使用background-attachment:fixed属性，页面滚动时，元素会出现上下抖动的问题
css
```
html{
    overflow:hidden;
    height: 100%;
}
body{
    overflow:auto;
    height: 100%;
}
```
https://www.coffeecup.com/help/articles/solving-the-ie11-fixed-background-bug/
https://stackoverflow.com/questions/27966735/why-does-a-fixed-background-image-move-when-scrolling-on-ie