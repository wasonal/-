### 函数
按值传递的参数
ECMAScript中所有函数的参数都是**按值传递**的   
主要区别在于引用类型参数上，对比下面两个例子
```
function setName(obj){
    obj.name = "Nick";
}
var person = new Object();
setName(person);
alert(person.name);// "Nick"
```
```
function setName(obj){
    obj.name = "Nick";
    obj = new Object();
    obj.name = "Tom";
}
var person = new Object();
setName(person);
alert(person.name);// "Nick"
```
用过c语言的同学对此肯定会非常的疑惑，第二段代码中的obj不是被重新声明了吗，为什么name还是Nick而不是Tom。回归到按值传递这个四个字，就可以理解这种"怪异"的行为了。因为是按值传递，所以传递进去的是obj在内存中的引用（地址），在obj重新声明的时候，obj换成了一个新的对象的地址，所以这时的obj不是彼时的obj了

函数参数arguments
1. 类数组
2. 可以用来实现重载
3. 与参数同步
```
function add(num1, num2){
    arguments[1] = 10;
    alert(num2);// 10
}
```
这个例子中，num2的值alert为10，因为在上一步我们给arguments[1]赋值为10，而num1 也会随之同步更新为10，但arguments[1]使用的内存空间和num2并不一样