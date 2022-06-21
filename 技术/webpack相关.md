# webpack 安装

首先需要安装Node.js, node.js自带软件包管理工具npm

查看node版本

> node -v

全局安装webpack

> npm install webpack@3.6.0 -g

本地安装webpack

> 在项目目录下执行
>
> `npm install webpack@3.6.0 --save-dev`

# webpack的基本使用



## 项目文件目录:

> - 项目
>
>   - dist     //打包好的文件
>
>   - src      //项目源码



## webpack 打包js文件

### 常规方式

> 在项目文件夹下
>
> ~~~bash
> webpack ./src/main.js ./dist/bundle.js
> ~~~
>
>  

### 简洁的方式

在项目目录下创建webpack.config.js文件

~~~js
//从node中引入包内容
//在使用前需要在项目目录执行`npm init`命令
const path = require('path')

module.exports = {
  //入口
  entry:'./src/main.js',
  //出口
  output: {
    //动态获取路径
    //用于拼接两个变量
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
}

//便捷打包方式:直接在命令行输入'webpack',就可以执行打包命令
~~~



### 更高效的方式

1. 在项目目录下执行命令:

   `npm init`

2. 修改package.json文件

   ~~~json
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1",
   
   //使用 npm run build执行
   //会优先使用本地版本webpack
       "build": "webpack"
     },
   ~~~

   

## loader

### 安装loader

#### 配置loader

**修改在项目目录下的webpack.config.js文件**

在module.exports中添加以下部分

~~~js
  //css-loader
  module: {
    rules: [
      {
        test: /\.css$/,
        //css-loader 只负责将css文件进行加载
        //style-loader负责将样式添加到DOM中
        //使用多个loader时,是从右向左读取的
        use: [ 'style-loader', 'css-loader'],
      },
    ],
  },
~~~



### 安装css-loader

以下命令默认安装最新版本的css-loader

`npm install --save-dev css-lader`



> 在mac中,由于安装的webpack3.6.0版本,直接执行以上命令,容易出现错误(版本不匹配):

![image-20220311172138730](/Users/cobb/Library/Application Support/typora-user-images/image-20220311172138730.png)

指定版本安装方法:

`npm install --save-dev css-loader@0.28.11`



### 安装style-loader

安装最新版本的:

`npm install style-loader --save-dev`



安装webpack3.6.0适配版本style-loader

`npm install --save-dev style-loader@0.15.0`



### less文件处理

安装对应webpack3.6.0版本的less和less-loader

`npm install --save-dev less-loader@5.0.0 less@3.13.1`



### 图片文件处理

安装url-loader

`npm install --save-devurl-loader@1.1.2`

> 在webpack.config.js文件中添加如下部分:
>
> ~~~js
>       {
>         test: /\.(png|jpg|gif|jpeg)$/i,
>         use: [
>           {
>             loader: 'url-loader',
>             options: {
>               //当加载的图片,小于limit时,会将图片编译成base64字符串的形式
>               //当加载的图片大于limit时,需要使用file-loader模块进行加载
>               limit: 50000,
>               //在dist文件夹下生成img文件夹以及和原图片同名的文件 
>               name: 'img/[name].[hash:8].[ext]'
>             },
>           }
>         ]
>       }
> ~~~
>
> 



### ES6转ES5语法

使用babel-loader



### 引入vue.js

#### 通过npm安装vue

- 因为在后续的实际项目中也会使用vue,所以并不是开发时依赖,不用加**-dev**

~~~bash
npm install vue --save
~~~



- 在js文件中引入vue

~~~js
import Vue from vue
~~~

- 出现runtime-only错误:

  原因:

  1. runtime-only,代码中不可以有任何的template
  2. runtime-compiler,代码中可以有template,因为有compiler可以编译template

  解决办法:在webpack.config.js文件中添加如下:

~~~js
  resolve:{
    alias:{
      'vue$': 'vue/dist/vue.esm.js'
    }
~~~



#### vue应用中'el'和'template'区别

template会将el中的内容进行替换



#### 正确使用vue的方式

- 安装vue-loader和vue-template-compiler

- 配置webpack.config.js

  ~~~js
   {
          test: /\.vue$/,
          use: ['vue-loader']
        }
  ~~~

- 在src文件夹下创建vue文件夹

  ![image-20220312151241214](/Users/cobb/Library/Application Support/typora-user-images/image-20220312151241214.png)

# Plugin

## 添加版权的plugin

使用bannerplugin插件,webpack自带插件

修改webpack.config.js文件



## 打包html的plugin

> HtmlWebpackPlugin插件可以做的事情:
>
> - 自动打包生成一个index.html文件(可以指定模板来生成)
> - 将打包的js文件,自动通过script标签插入到bady中

安装之后配置webpack.config.js文件如下:

~~~js
      new HtmlWebpackPlugin({
        //根据以下模板生成
        template: `index.html`
      })
~~~



## js压缩的Plugin

使用第三方的插件Uglifyjs-webpack-plugin

需要指定版本号1.1.1,保持和CIL2一致

`npm install --save-dev uglifyjs-webpack-plugin@1.1.1`



# 搭建本地服务器

- 这个本地服务器基于node.js,内部使用express框架,可以实现浏览器自动刷新显示修改后的结果

- 安装: `npm install --save-dev webpack-dev-server@2.9.3`

- 设置:

  - devserver也是作为webpack中的一个选项,可以设置如下属性:

    ~~~js
    contentBase:为哪一个文件夹提供本地服务
    port:端口号 
    inline:页面实时刷新 
    historyApiFallback:在SPA页面中,依赖html5的history模式
    ~~~

    

- 启动方式:

  - 在package.json文件中添加: `"dev": "webpack-dev-derver"`
    - 在后面添加 ` --open` ,能够在启动服务器的同时自动打开浏览器
  - 在终端中输入: `npm rundev`

- ### webpack配置的分离

  - 首先对webpack.config.js文件进行抽离,分成三部分:
    - base.config.js
    - dev.config.js
    - prod.config.js
  - 安装-**webpack-merge**插件,实现config文件的两两合并
  - 在package.json文件中修改"build"和"dev"的运行路径
  - 

















# BUG记录

1. 安装npm出现错误:

   ~~~bash
   npm ERR! code EACCES
   npm ERR! syscall rename
   npm ERR! path /usr/local/lib/node_modules/npm
   npm ERR! dest /usr/local/lib/node_modules/.npm-i9nnxROI
   npm ERR! errno -13
   npm ERR! Error: EACCES: permission denied, rename '/usr/local/lib/node_modules/npm' -> '/usr/local/lib/node_modules/.npm-i9nnxROI'
   npm ERR!  [Error: EACCES: permission denied, rename '/usr/local/lib/node_modules/npm' -> '/usr/local/lib/node_modules/.npm-i9nnxROI'] {
   npm ERR!   errno: -13,
   npm ERR!   code: 'EACCES',
   npm ERR!   syscall: 'rename',
   npm ERR!   path: '/usr/local/lib/node_modules/npm',
   npm ERR!   dest: '/usr/local/lib/node_modules/.npm-i9nnxROI'
   npm ERR! }
   npm ERR!
   npm ERR! The operation was rejected by your operating system.
   npm ERR! It is likely you do not have the permissions to access this file as the current user
   npm ERR!
   npm ERR! If you believe this might be a permissions issue, please double-check the
   npm ERR! permissions of the file and its containing directories, or try running
   npm ERR! the command again as root/Administrator.
   
   npm ERR! A complete log of this run can be found in:
   npm ERR!     /Users/cobb/.npm/_logs/2022-03-10T13_55_54_267Z-debug.log
   ~~~

   解决办法:

   需要在命令前加上 ==sudo==

2. 