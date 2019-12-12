null，undefined，void都是类型
声明一个void类型的变量智能将它赋值为undefined和null
与void的区别是undefined和null是所有类型的子类型
即undefined类型的变量可以赋值给number类型的变量
```
// 不会报错
let num: number = undefined
// 这样也不会报错
let u:undefined;
let num: number = u;
// void类型的变量不能赋值给Number类型的变量
let u:void;
let num: number = u;// Type 'void' is not assignable to type 'number'
```