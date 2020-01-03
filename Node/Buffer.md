Buffer是一个js与C++结合的模块，是一个类Array的对象，其元素是16进制的两位数，主要用于操作字节，例如:
let str: string = "深入浅出node.js"
let buf: Buffer = new Buffer(str, 'utf-8')
console.log(buf)
// <Buffer e6 b7 b1 e5 85 a5 e6 b5 85 e5 87 ba 6e 6f 64 65 2e 6a 73>
除了以保存数据和字符编码为参数的实例化方式，Buffer还可以声明字节长度的方式实例化
let buf:Buffer = new Buffer(100)
console.log(buf.lenght); // 100
这种初始化方式生成的Buffer对象的元素为0到255的随机值
然后我们还可以给元素赋值，赋值的规律为：小于0就加256到0-255；大于255，就减256到0-255，小数则舍弃小数部分

Buffer的内存不是在V8的堆内存中，而是通过C++实现内存申请的
处理大量字节数据的时候如果采用需要多少内存就向系统申请多少内存的策略，可能造成大量的内存申请的系统调用，所以Buffer在C++申请内存，在js中分配内存的策略，而为了高效地使用申请来地内存，采用了slab动态内存管理机制
slab是一块固定大小的内存区域，它有三种状态：完全分配，部分分配，没有分配
小对象(小于8KB)：slab的大小为8KB，小对象会被放进slab中直至装不下然后申请另一块同样为8KB的slab，对于其中一块slab来说，只有其中的对象都被回收后，这块slab才可以释放
大对象(大于等于8KB)：直接申请一块与大对象大小相同的slab内存独占

Buffer的转换
字符串转Buffer:new Buffer(str, [encoding])
Buffer转字符串:buf.write(string, [offset], [length], [encoding])
对于Buffer不支持的编码形式，可以借助conv和iconv-lite来进行扩展

concat方法:接受buf片段的数组和片段的总长度然后生成一个合并的Buffer对象
