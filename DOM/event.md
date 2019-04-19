### DOM事件流(event的传递方式)
捕获阶段（自顶向下）->目标阶段->冒泡阶段（自下而上）->默认事件   
```
<html>
  <head> </head>

  <body>
    <div id="parentDiv">
      <a id="childButton" href="https://github.com"> click me! </a>
    </div>
  </body>
</html>
```
当我们点击上面这段html代码中的a标签时，浏览器会首先计算出从a标签到html标签的节点路径(html->body->div->a)    
然后进入捕获阶段，依此触发注册在html->body->div->a上的捕获类型的点击事件    
然后触发绑定在onXXX属性上的handler    
到达a节点后进入冒泡阶段，依此触发a->div->body->html上注册的冒泡类型的点击事件    
最后冒泡阶段到达html节点后，会触发浏览器的默认行为（对于a标签来说就是跳转页面）
