### let
1. 暂时性死区
2. 对于for循环，设置循环变量的部分是父作用域，循环体内部是一个单独的子作用域
```
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```
而且每次迭代循环时都创建一个新变量，并以之前迭代中同名变量的值将其初始化
即这样一段代码
```
var funcs = [];
for (let i = 0; i < 3; i++) {
    funcs[i] = function () {
        console.log(i);
    };
}
```
等同于
```
// 伪代码
(let i = 0) {
    funcs[0] = function() {
        console.log(i)
    };
}

(let i = 1) {
    funcs[1] = function() {
        console.log(i)
    };
}

(let i = 2) {
    funcs[2] = function() {
        console.log(i)
    };
};
```
3. 不存在变量提升
4. 不允许重复声明

不仅仅是变量，函数也有了自己的块级作用域

### const
声明一个只读的常量，这意味着const一旦声明就必须立即初始化。
const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。