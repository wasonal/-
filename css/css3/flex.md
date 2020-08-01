## 用flex设置间隔均匀排列,最后一排左对齐
```
.father{
    display: flex;
    justify-content: space-between;
}
.son{
    margin-left: auto;
}
```

## flex布局实现最后一个子元素右对齐
```
<style>
    .outer{
        display: flex;
    }
    .outer div:last-child{
        margin-left: auto;
    }
</style>

<div class="outer">
    <div>left</div>
    <div>center</div>
    <div>right</div>
</div>
```