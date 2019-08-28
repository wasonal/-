定义
new运算符的原理
1、创建一个空对象暂且称为o
2、将o的proto指向构造函数的prototype
3、以o对象为构造函数的this，执行构造函数
4、如果构造函数有返回值则返回这个返回值，如果没有则返回o对象

new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型实例

用new Object() 的方式新建了一个对象 obj
取出第一个参数，就是我们要传入的构造函数。此外因为 shift 会修改原数组，所以 arguments 会被去除第一个参数
将 obj 的原型指向构造函数，这样 obj 就可以访问到构造函数原型中的属性
使用 apply，改变构造函数 this 的指向到新建的对象，这样 obj 就可以访问到构造函数中的属性
返回 obj

```
function ObjectCreate(){
        var obj = {};
        var Constructor = Array.prototype.shift.call(arguments);
        obj.__proto__ = Constructor.prototype;
        var ret = Constructor.apply(obj, arguments);
        return typeof ret === 'object' ? ret : obj;//如果构造函数有返回值的话以返回值为最终结果
    }
```