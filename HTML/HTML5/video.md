### video标签
#### 用途
用于在HTML中嵌入媒体播放器
```
<video controls width="250">
    <source src="/media/flower.webm" type="video/webm">
    <source src="/media/flower.mp4" type="video/mp4">
    <p>
        Sorry,your brower does not support embedded  videos, here is a <a href="/   media/flower.mp4">link to the video</a> instead.
    </p>
</video>
```
浏览器支持的视频格式不相同，所以我们可以在<source>元素中提供多个视频源，然后浏览器将会使用它第一个支持的源
#### 注意
>* ```controls```属性定义视频是否展示浏览器自带的控件，我们可以用JavaScript和相关的API创建控件
>* ```<track>```元素和webvtt格式让我们可以用JavaScript在视频中展示字母或标题
>* video设置了loop循环属性之后在几次循环后会自动暂停，原因暂定为chrome对于视频循环占用内存的处理，实现循环可以使用ended事件+video.play()
#### 相关属性
属性名|描述
:--|:--
autoplay|视频马上开始自动播放
controls|允许用户控制视频的相关属性
loop|是否循环
muted|属性值为true时视频音频静音
preload|定义视频缓存的时机,```none```视频不需缓存，```metadata```抓取元数据（长度），```auto```视频需缓存
poster|封面图的url
src|嵌入到视频的url（可以用source）