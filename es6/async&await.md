## async 函数|函数表达式|lambda表达式
async/await实际上是Generator函数的语法糖：async替代Generator函数的星号(*)，await替代yield      
async返回一个Promise对象，如果是return 直接量，async会把这个直接量通过Promise.resolve()封装成Promise对象
作用
使用方法
注意事项
和Promise的区别
## await 函数|Promise|直接量
> 如果await的是Promise，那么就会阻塞后面的代码，等着Promise对象resolve的值为运算结果（阻塞被封装到一个Promise中异步执行）
> 如果不是Promise，那么就会执行并返回运算的结果
## async/await对于Generator函数的优势
> （1）内置执行器
> （2）更好的语义
> （3）更广的适用性
## 注意点
await命令后面的Promise对象运行结果可能是reject，所以最好把await命令放在try...catch代码块中
```
async function myFunction() {
  try {
    await somethingThatReturnsAPromise();
  } catch (err) {
    console.log(err);
  }
}

// 另一种写法

async function myFunction() {
  await somethingThatReturnsAPromise().catch(function (err){
    console.log(err);
  });
}
```