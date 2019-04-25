Ajax技术这一技术 能够向服务器请求额外的数据而无须卸载页面
Ajax技术的核心——XMLHttpRequest对象，简称XHR
```
var request;
if(window.XMLHttpRequest){
    request = new XMLHttpRequest();IE7+及其他浏览器
}else{
    request = new ActiveXObject('Microsoft.XMLHTTP');//IE5,IE6
}
request.ontimeout = function(){//为request绑定timeout事件
    console.log('the req time out');
}
request.withCredentials = true;//设置跨域请求为提供凭证信息（cookie，HTTP认证及客户端SSL证
//明等），也可以简单地理解为当前请求为跨域类型是是否在请求中写代cookie。
//当配置了为true时，必须要在后端添加response头信息Access-Control-Allow-Origin并且配置为
//请求域名
request.timeout = 1000；//设定request的时间限制为1秒
request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');//设置请求头
request.onreadystatechange = function(){//为request绑定onreadystatechange事件
    if(request.readyState == 4 && request.status == 200){
        request.responseText;//获取字符串形式的响应数据
        request.responseXML;//获取XML形式的响应数据
        do something;
    }
}
request.open(method, url, async是否异步);
request.send(data);data仅用于post请求
```
readyState存有XHR对象的状态，从0-4发生变化
0: 请求未初始化；1: 服务器连接已建立；2: 请求已接收；3: 请求处理中；4: 请求已完成，且响应已就绪
status属性存有XHR对象的状态码
```
var xhr = new XMLHttpRequest();//xhr.readyState = 0,XMLHttpRequest已初始化
xhr.open(method, url, true);//xhr.readyState = 1，open方法已被触发，可以通过setRequestHeader()设置请求头，responseType设置返回值类型(默认为DOMString)
xhr.send(null);//xhr.readyState = 2，send方法被调用
//3，请求处理中
//4，请求完成，意味着数据传输彻底完成或失败
```