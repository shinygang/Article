## Webpack是什么
首先可以看下[官方文档](http://webpack.github.io/), [这里](https://github.com/petehunt/webpack-howto)国外的一个朋友有介绍。Webpack是由Tobias Koppers开发的一个开源前端模块构建工具。它的基本功能是将以模块格式书写的多个JavaScript文件打包成一个文件，同时支持CommonJS和AMD格式。但让它与众不同的是，它提供了强大的loader API来定义对不同文件格式的预处理逻辑，从而让我们可以将CSS、模板，甚至是自定义的文件格式当做JavaScript模块来使用。Webpack 基于loader还可以实现大量高级功能，比如自动分块打包并按需加载、对图片资源引用的自动定位、根据图片大小决定是否用base64内联、开发时的模块热替换等等，可以说是目前前端构建领域最有竞争力的解决方案之一。
![作用](http://images2015.cnblogs.com/blog/255104/201512/255104-20151209195325824-1318342518.png)

## 为什么使用Webpack
* 他类似browserify 但是可以把你的应用分离成许多文件，如果你有许多页面在你的单页应用里面，用户只需要下载当前页面所需要的代码。如果你跳转到另一个页面，他们不需要重新加载通用的代码。
* 他能替代grunt或者gulp大部分的功能 因为他可以构建和打包CSS，预处理CSS，编译JS和打包处理图片，甚至更多事情。
* 他支持AMD和CommonJs以及其他的模块化系统（Angular，ES6）。如果你不知道用什么，那么可以用CommonJs。

## 怎么安装Webpack
#### 安装node.js
首先需要安装[Node.js](https://nodejs.org/)，node自带了包管理工具`npm`。
#### 安装webpack
使用`npm install webpack -g`，webpack全局安装到了本地环境中，就可以使用`webpack`命令了。
#### 在项目中使用webpack
* 通过`npm init`实例化package.json文件。
* 通过`npm install webpack --save-dev`安装`webpack`到`package.json`文件中。
* 或者通过`npm install webpack@1.2.x --save-dev`安装指定版本的`webpack`到`package.json`文件中。
* 通过`npm install webpack-dev-server --save-dev`安装`dev tools`到`package.json`文件中，本地运行webpack服务。

## 怎么使用Webpack
1、安装`webpack`后，可以使用`webpack`这个命令行工具。主要命令：`webpack <entry> <output>`。可以切换到包含webpack.config.js的目录运行命令：
* `webpack` 执行一次开发时的编译
* `webpack -p` 执行一次生成环境的编译（压缩）
* `webpack --watch` 在开发时持续监控增量编译（很快）
* `webpack -d` 让他生成SourceMaps
* `webpack --progress` 显示编译进度
* `webpack --colors` 显示静态资源的颜色
* `webpack --sort-modules-by, --sort-chunks-by, --sort-assets-by` 将modules/chunks/assets进行列表排序
* `webpack --display-chunks` 展示编译后的分块 
* `webpack --display-reasons` 显示更多引用模块原因
* `webapck --display-error-details` 显示更多报错信息

2、每个项目下都必须配置有一个 `webpack.config.js`，它的作用如同常规的 `gulpfile.js/Gruntfile.js` ，就是一个配置项，告诉 webpack 它需要做什么。
下面看一个简单的示例：
```
var webpack = require('webpack');

module.exports = {
    //插件项
    plugins: [
	    //提公用js到common.js文件中
	    new webpack.optimize.CommonsChunkPlugin('common.js'),
	    //将样式统一发布到style.css中
	    new ExtractTextPlugin("style.css", {
	        allChunks: true,
	        disable: false
	    }),
	    //使用ProvidePlugin加载使用频率高的模块
	    new webpack.ProvidePlugin({
	        $: "webpack-zepto"
	    })
	],
    //页面入口文件配置
    entry: {
        index : './src/main.js'
    },
    //入口文件输出配置
    output: {
        path: __dirname +'/dist/',
        filename: '[name].js'
    },
    module: {
        //加载器配置
        loaders: [
            { test: /\.css$/, loader: 'style-loader!css-loader' },
            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},
            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
        ]
    },
    //其它解决方案配置
    resolve: {
        extensions: ['', '.js', '.json', '.scss'],
        alias: {
            filter: path.join(__dirname, 'src/filters')
        }
    }
};
```
#### entry
`entry`是页面入口文件配置，可以是一个文件或者多个入口文件，可以是对象格式或者数组格式。
```
entry: {
    index : './src/main.js'
} 
entry:['./src/main.js','./src/index.js']
```
#### output
`output` 是对应输出项配置,主要包括`path`,`filename`和`publishPath`属性。`path`代表输出的路径，`filename`代表输出的文件名称，`publishPath`代表静态资源发布后的前缀地址。
#### module.loaders
[module.loaders](http://webpack.github.io/docs/using-loaders.html) 是最关键的一块配置。它告知 webpack 每一种文件都需要使用什么加载器来处理。[点击这里可以查看loader list](http://webpack.github.io/docs/list-of-loaders.html)。
```
module: {
    //加载器配置
    loaders: [
	    //.css 文件使用 style-loader 和 css-loader 来处理
        { test: /\.css$/, loader: 'style-loader!css-loader' },
        //.scss 文件使用 style-loader、css-loader 和 sass-loader 来编译处理
        { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},
        //图片文件使用 url-loader 来处理，小于8kb的直接转为base64
        { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
    ]
}
```
loader主要有3种使用方式：
##### 1、在页面里面引用资源使用
* require("url-loader?mimetype=image/png!./file.png");
##### 2、在webpack.config.js文件夹中使用
* { test: /\.png$/, loader: "url?mimetype=image/png" };
##### 3、在命令行中编译使用
* webpack --module-bind "png=url-loader?mimetype=image/png";

如上，"-loader"其实是可以省略不写的，多个loader之间用“!”连接起来。
注意所有的加载器都需要通过 npm 来加载，并建议查阅它们对应的 readme 来看看如何使用。
拿最后一个 url-loader 来说，它会将样式中引用到的图片转为模块来处理，使用该加载器需要先进行安装：
npm install url-loader -save-dev
配置信息的参数“?limit=8192”表示将所有小于8kb的图片都转为base64形式（其实应该说超过8kb的才使用 url-loader 来映射到文件，否则转为data url形式）。也可以使用file-loader来加载资源文件。
#### plugins
[plugins](http://webpack.github.io/docs/using-plugins.html) 是插件项，这里我们使用了一个 CommonsChunkPlugin 的插件，它用于提取多个入口文件的公共脚本部分，然后生成一个 common.js 来方便多页面之间进行复用。[点击这里可以查看plugins list](http://webpack.github.io/docs/list-of-plugins.html)。
```
plugins: [
    //提公用js到common.js文件中
    new webpack.optimize.CommonsChunkPlugin('common.js'),
    //将样式统一发布到style.css中
    new ExtractTextPlugin("style.css", {
        allChunks: true,
        disable: false
    }),
    //使用ProvidePlugin加载使用频率高的模块
    new webpack.ProvidePlugin({
        $: "webpack-zepto"
    })
]
```
如上，包含两种：
1、第一种webpack自带的一些插件：`webpack.ProvidePlugin`、`webpack.optimize.CommonsChunkPlugin`，
2、另外一种则通过`npm`包安装的：`ExtractTextPlugin`。
#### resolve
最后是 resolve 配置，这块很好理解，直接写注释了：
```
resolve: {
    // require时省略的扩展名，如：require('module') 不需要module.js
    extension: ['', '.js'],
    //别名
    alias: {
        filter: path.join(__dirname, 'src/filters')
    }
}
```
## 使用Webpack-dev-server
[webpack-dev-server](http://webpack.github.io/docs/webpack-dev-server.html)是基于node.js Express服务，它同时包含了一个基于[Socket.IO](http://socket.io/)轻量的运行时环境。
```
'use strict'
var webpack = require('webpack');
var WebpackDevServer = require('webpack-dev-server');
var config = require('./webpack.config');
// 配置代码自动编译和热替换插件
config.entry.unshift('webpack-dev-server/client?http://localhost:9090', "webpack/hot/dev-server");
config.plugins.push(new webpack.HotModuleReplacementPlugin());
// 这里配置：请求http://localhost:9090/index.php，
// 相当于通过本地node服务代理请求到了http://testapi.uhouzz.com/index.php
var proxy = [{
    path: "/index.php/*",
    target: "http://pc.uhouzz.com",
    host: "pc.uhouzz.com"
}]
//启动服务
var app = new WebpackDevServer(webpack(config), {
    publicPath: config.output.publicPath,
    hot:true,
    historyApiFallback: true,
    proxy:proxy
});
app.listen(9090);
```
如上，引用`webpack`和`webpack-dev-server`模块，通过WebpackDevServer启动服务，通过`HotModuleReplacementPlugin`插件启动代码自动编译页面自动刷新。这样，当你修改了html、js或者样式文件，页面会自动编译刷新。
## html页面使用
直接在页面引入 webpack 最终生成的页面脚本和样式文件即可。
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>webpack test</title>
    <link rel="stylesheet" href="/dist/style.css">
</head>

<body>
    <div id="app"></div>
    <script src="/dist/common.js"></script>
    <script src="/dist/build.js"></script>
</body>
</html>
```
## 总结
基于 webpack 的入门教程就到这里，希望本文能对你有所帮助，你也可以参考下面的项目进行参考。
[Vue-cnodejs](https://github.com/shinygang/Vue-cnodejs),基于Vue.js重写的cnodejs的webapp,其中采用的webpack进行打包处理。
