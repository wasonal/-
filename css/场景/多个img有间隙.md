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