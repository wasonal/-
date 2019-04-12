# eval函数
## 语法
**eval(string)**   
string表示JavaScript表达式，语句或一系列语句的字符串。表达式可以包含变量以及已存在对象的属性   
## 返回值
>* 参数是整数或者函数，直接返回该整数或函数
>* 参数是字符串，且字符串是表达式，则执行该字符串并返回表达式的运行结果
>* 参数是字符串，且字符串是JSON格式（此时的JOSN格式外面要加上**一对小括号**将JSON包围起来）
>* 参数是字符串，且字符串是语句或语句块，则执行该语句块并返回undefined
## 作用域
1. 直接调用   
eval直接在函数内部使用，此时eval的作用域是局部作用域   
```
function foo(){
    eval("var a=1;");
}
foo();
console.log(a);//报错a未声明
```
2. 间接调用
将eval赋值给另外一个变量，然后执行，此时eval的作用域是全局作用域
```
function foo(){
    var fakeEval=eval;
    fakeEval("var a=1;");
}
foo();
console.log(a);//1
```
3. 作为window对象的属性调用
强调window.eval来执行string，此时eval的作用域是全局作用域
```
function foo(){
    window.eval("var a=1;");
}
foo();
console.log(a);//1
```
## 严格模式
严格模式下eval会创建eval作用域，即为eval中的代码块新建一个作用域，而不是像在正常模式下使用全局作用域或局部作用域   
```
function foo(){
    "use strict";
    eval("var a=1;");
    console.log(a);//严格模式下报错，正常模式下输出1
}
foo();
```
自己做了个测试，发现严格模式会创建eval作用域是针对直接调用来说的；   
当使用间接调用的时候，eval还是使用全局的作用域
```
function foo(){
    "use strict";
    window.eval("var a=1;");
}
foo();
console.log(a);//不报错，而是输出1
```