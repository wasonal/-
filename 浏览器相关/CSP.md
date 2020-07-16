# CSP内容安全策略(Content-Security-Policy)
通过设置CSP可以规定对某种类型资源的加载使用安全策略，且可以设置CSP违规报告来监视攻击者
## 使用
在HTTP Header上使用（首选）
```
1. "Content-Security-Policy:" 策略
2. "Content-Security-Policy-Report-Only:" 策略
```
在HTML上使用
```
1. <meta http-equiv="content-security-policy" content="策略">
2. <meta http-equiv="content-security-policy-report-only" content="策略">
```
## 策略写法
```
// 限制所有的外部资源，都只能从当前域名加载
1. Content-Security-Policy: default-src 'self'
```
相关配置https://blog.csdn.net/qq_37943295/article/details/79978761
