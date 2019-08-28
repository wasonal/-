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

var arrayLike = {0: 'name', 1: 'age', 2: 'sex', length: 3 }
// 1. slice
Array.prototype.slice.call(arrayLike); // ["name", "age", "sex"] 
// 2. splice
Array.prototype.splice.call(arrayLike, 0); // ["name", "age", "sex"] 
// 3. ES6 Array.from
Array.from(arrayLike); // ["name", "age", "sex"] 
// 4. apply
Array.prototype.concat.apply([], arrayLike)