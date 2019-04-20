## for
for用于创建一个循环
```
//遍历数组
var arr = [1,2,3];
for(var i=0; i<arr.length; i++){
    console.log(arr[i]);
}
```
上述代码执行顺序是
1. 初始化i=0;
2. 判断i小于arr.length为真，打印arr[0]，1，执行i++;
3. 判断i小于arr.length为真，打印arr[1]，2，执行i++;
4. 判断i小于arr.length为真，打印arr[2]，3，执行i++;
5. 判断i小于arr.length为假，退出循环
Tip:判断语句在每一次执行循环体前都会进行一次计算
## for in 
for...in语句以**任意顺序**（不论是数组还是其他对象）遍历一个对象自有的、可枚举的、**继承的、非Symbol**的属性
> for(var variable in object){...}
variable：在每次迭代时，将不同的属性名分配给此变量   
object：被迭代枚举属性的对象
```
var obj = {
    name: 'xiaoming',
    age: '0'
}
for(var key in obj){
    console.log(key);
}
// 依次输出'name','age'
```
## for of
在可迭代对象（包括Array,Map,Set,String,argument对象等等）上创建一个迭代循环，调用代码块，并未每个不同属性的值执行语句
> for(var variable of object){...}
```
function *foo(){
    yield 1;
    yield 2;
}

for(let value of foo()){
    console.log(value);
}
//依次输出1,2
```
如果想要遍历对象属性，可以结合Object.keys(obj)
```
var obj = {
    name: 'xiaoming',
    age: '0'
}
for(var key of Object.keys(obj)){
    console.log(key);
}依此输出'name','age'
```
for,for...in,for...of均可使用break,continue来跳出循环
## 总结
遍历值
> for...in遍历的是对象可迭代，自身或继承的属性名
> for...of遍历的是可迭代对象（set,map,array,类数组对象）的键值
遍历顺序
for...in和for...of的遍历顺序都是不规则的，由浏览器决定