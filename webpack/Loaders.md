## 资源路径
### file-loader
作用：1、解决项目中的路径问题；2、让webpack识别资源文件   
原理：由于webpack会将各个模块打包成一个文件，最终样式中的url是相对入口html页面的，而不是相对于原始路径，这就会导致一些资源引入失败   
file-loader可以解析项目中的url，会根据配置将图片拷贝到相应的路径，打包时会根据规则引入路径。
### url-loader
file-loader的一个超集    
作用：1、解决项目中的路径问题；2、让webpack识别资源文件；3、将小体积的资源转换成base64
将html以及css中的图片打包成base64，但是js中如果有图片url并不能编译成功
### html-withimg-loader