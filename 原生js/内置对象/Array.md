判断一个值是否为数组
```
function isArray(testValue){
    return Object.prototype.toString.call(testValue) === "[object Array]";
}
```

# Array
## fill方法
Array.prototype.fill(value[, start[, end]])用一个固定值填充一个数组中从起始索引到终止索引内的全部元素   
value：填充值   
start：填充起始位置，可以省略   
end：填充结束位置，可以省略，实际结束位置是end-1   
返回值：填充后的数组   