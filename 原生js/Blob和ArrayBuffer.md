# Blob对象：只读原始数据的类文件对象
File对象继承自Blob对象
# ArrayBuffer对象：通用固定长度的原始二进制数据缓冲区
可以通过new ArrayBuffer(length)来获得一片连续的内存空间，它不能直接读写
可根据需要将其传递到TypedArray视图或DataView对象来解释原始缓冲区   
## TypedArray
需指定一个数据类型来保证数组成员都是同一数据类型

## DataView

# 异同联系
Blob与ArrayBuffer的区别是：除了原始字节外它还提供了mime type作为元数据   
二者可以互相转换

# 例子
## 创建Blob对象并转换成ArrayBuffer
```
const text = "<div>hello world</div>";
//创建以二进制数据存储的html文件
const blob = new Blob([text], {type: "text/html"});
//以文本形式读取
const textReader = new FileReader();
textReader.readAsText(blob);
textReader.onload = function(){
    console.log(textReader.result);    
}
```