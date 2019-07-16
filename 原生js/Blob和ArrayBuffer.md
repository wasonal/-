之前面试被问到怎么做一个图片裁剪工具，逛博客刚好看到这篇文章，里面的blob和arraybuffer的知识是做图片裁剪工具的一部分，就再学习一下（水真深），还有一些东西还没有写完，后续再补充
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

# 实战
## 图片预览
video标签，audio标签还是img标签的src属性，不管是相对路径，绝对路径，或者一个网络地址，归根结底都是指向一个文件资源的地址。
html
```
<input id="upload" type="file" />
<img id="preview" src="" alt="预览" />
```
javascript
```
const upload = document.querySelector("#upload")
const preview = document.querySelector("#preview")
upload.onchange = function(){
    const file = this.files[0]
    const src = URL.createObjectURL(file)
    preview.src = src;
}
```