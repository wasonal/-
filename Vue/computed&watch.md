### computed
1. 普通形式
```
<p>你的总分是{{score}}</p>

computed(){
    score(){
        return this.math + this.english;
    }
}
```
其实就是给math和english的setter加上这个函数
而这个score依赖的变量math和english是会被缓存起来的   
所以有math，english发生变化之后才会分别对他们重新计算
否则返回的是上一次缓存的值

而如果使用的是触发方法来对它进行计算，那么每次都会触发所有变量的getter

参考链接: https://www.cnblogs.com/gunelark/p/8492468.html
https://www.w3cplus.com/vue/vue-computed-intro.html