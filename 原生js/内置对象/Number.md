isFinite(testValue)
判断testValue是否是有限数字或（可转换为有限数字），是则返回true，否则如果testValue是NaN或者正、负无穷大的数，则返回false。
```
//判断是否为数字
function isNumber(testValue){
    return typeof testValue === "number" && isFinite(testValue);
}
```
