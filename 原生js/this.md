this 是在运行时进行绑定的，和函数声明的位置没有任何关系，只取决于函数的调用方式

function foo() {
console.log( this.a );
}
var a = 2;
(function(){
"use strict";
foo(); // 2
})();
对比
function foo() {
"use strict";
console.log( this.a );
}
var a = 2;
foo(); // TypeError: this is undefined

绑定规则
1、默认绑定，方法自执行
2、隐式绑定，作为对象属性执行，或者在有上下文的环境执行
3、call、apply显式调用
4、new绑定
5、事件绑定时this的执行：哪个DOM元素触发事件，this就指向哪个DOM元素
function foo() {
console.log( this.a );
}
var obj = {
a: 2,
foo: foo
};
obj.foo(); // 2