# XSS跨站脚本攻击
## 原理
恶意攻击者利用网站没有对用户提交数据进行转义处理或者过滤不足的缺点，进而添加一些代码，嵌入到web页面中去。使别的用户访问都会执行相应的嵌入代码。
## 分类
### 反射型
举例子
1. 有一个使用get请求的搜索接口url，url后会加上搜索关键词，且关键词会显示到搜索后的页面
2. 黑客A给B发送恶意链接，并在该url后加上一段自己的恶意脚本
3. B在浏览器访问该url后，这段在url后的script就会执行

**防御**：此类 XSS 通常出现在网站的搜索栏、用户登录口等地方，需要后端对html，css，JavaScript进行过滤，可以使用encodeURIComponent对字符进行转义
### 持久型
举例子
1.有一个博客可以进行评论
2.黑客A发表用script标签包裹的代码
3.发布成功后每一个访问该该页面的用户都会自动执行这段代码
**危害**
>* 盗取cookie
>* Dos攻击
>* 使用js或css破坏页面结构或样式

**防御**：
1. 对cookie设置httpOnly，客户端就无法通过document.cookie来获取cookie
2. 前端数据传递给服务器之前，先转义/过滤(防范不了抓包修改数据的情况)
3. 服务器接收到数据，在存储到数据库之前，进行转义/过滤
4. 前端接收到服务器传递过来的数据，在展示到页面前，先进行转义/过滤

### DOM型
原理：前端的JavaScript代码不够严谨，把不可信的内容插入到页面。比如使用.innerHTML、.outerHTML等API的时候   
**防御**：
1. 对于url链接，例如src属性，可以直接使用encodeURIComponent来进行转义
2. 非url，我们可以这样进行编码
```
    function encodeHtml(str){
        return str.replace(/"/g, '&quot;')
                  .replace(/'/g, '&apos;')
                  .replace(/</g, '&lt;')
                  .replace(/>/g, '&gt;');
    }
```
### Content-Security-Policy（CSP）
HTTP 响应头Content-Security-Policy允许站点管理者控制用户代理能够为指定的页面加载哪些资源。