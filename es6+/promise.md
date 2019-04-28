## Promise
### 链式调用
```
//p1,p2,p3均为Promise对象
p1.then((data)=>{
    console.log(data);
    return p2;
}).then((data)=>{
    console.log(data);
    return p3;
})
```
### 方法
#### Promise.all(iterable)「谁跑的慢，以谁为准执行回调」
用于将多个Promise实例包装成一个新的Promise实例   
**返回值**   
> 成功：结果数组
> 失败：最先被reject失败状态
```
let p1 = new Promise(function(resolve, reject){
    resolve('success 1');
});
let p2 = new Promise(function(resolve, reject){
    resolve('success 2');
});
let p3 = new Promise(function(resolve, reject){
    reject('fail');
});
Promise.all([p1,p2]).then((result)=>{
    console.log(result);//输出['success 1','success 2']
}).catch((error)=>{
    console.log(error);
})
Promise.all([p1,p2,,p3]).then((result)=>{
    console.log(result);
}).catch((error)=>{
    console.log(error);//输出'fail'
})
```
应用场景：一个页面上需要等待两个或多个ajax的数据回来以后才正常显示   
**简单实现**
```
Promise.prototype.fakeAll = function(promiseArr){
    return Promise(function(resolve, reject){
        var resolveCounter = 0;//返回值计数器
        var promiseLen = promiseArr.length;
        var resolveValues = new Array(promiseLen);//返回数组
        for(var i=0; i<promiseLen; i++){
            (function(i){
                Promise.resolve(promiseArr[i]).then(function(value){
                    resolveCounter++;
                    resolveValues[i] = value;
                    if(resolveCounter == promiseLen){
                        return resolve(resolveValues);
                    }
                },function(error){
                    return reject(reason);
                })
            })(i)
        }
    })
}
```
#### Promise.race(iterable)「谁跑的快，以谁为准执行回调」
返回多个Promise实例中返回最快的实例
```
let p1 = new Promise((resolve,reject)=>{
    setTimeout(()=>{//模拟异步请求
        resolve('success');
    }, 300);
});
let p2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{//模拟异步请求
        reject('fail');
    }, 500);
});
Promise.race([p1,p2]).then((result)=>{
    console.log(result);//输出success
}).catch((error)=>{
    console.log(error);
})
```
应用场景：可以给某个异步操作设置超时时间，并且在超时后执行相应的操作

### return,resolve,reject
在Promise中的resolve或reject，仅仅是将Promise的状态置为fulfilled或rejected，并没有结束当前的代码，如果后续有代码的话会继续执行，例子如下
```
function foo(){
    return new Promise(function(res, rej){
        res(1);
        console.log(3);
        return 2;
    })
}
var p1 = foo();
p1.then((data)=>{
    console.log(data);
}).catch((err)=>{
    console.log(err);
}).finally((data)=>{
    console.log(data);
})
//输出3 1 undefined
```

参考链接：[https://blog.csdn.net/qq_36850813/article/details/80528663](https://blog.csdn.net/qq_36850813/article/details/80528663)