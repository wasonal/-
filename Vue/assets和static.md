首先需要了解webpack如何处理静态资产，在```*.vue```组件中，所有模板和css都会被```vue-html-loader```及```css-loader```解析并查找资源URL。例如在```<img src="./logo.png">```中```"logo.png"```是相对的资源路径，将由**webpack解析为模块依赖**   
由于```logo.png```不是JavaScript，当被时为模块依赖时，需要使用```url-loader```和```file-lodaer```处理。而vue-cli的webpack脚手架已经配置了这些loader，因此可以使用相对/模块路径。   
