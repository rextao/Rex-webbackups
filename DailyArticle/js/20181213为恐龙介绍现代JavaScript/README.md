# 概述
1. https://medium.com/the-node-js-collection/modern-javascript-explained-for-dinosaurs-f695e9747b70
2. 20171019
3. 目标是：从html，JavaScript开发网页，开始是手动网上搜索js引入到html，通过npm自动引入第三方库，通过模块绑定器（webpack）构建单一文件，通过转义器（babel）使用更先进的js语法，利用npm scripts实现脚本自动化。 

## 读后总结

1. 给新手的，综述npm，webpack，babel，run scripts都给干嘛的
2. 搞了个webpack例子

## 原始方式使用js

1. 正常使用js方式是在页面中使用script引入js文件
2. 比如想用一个时间处理的js库，需要去官网moment.js，下载最新的js
3. 这样的问题是：每次更新新版本时，查找和下载都很烦人

## 包管理器npm

1. 为解决上述问题，出现了众多的包管理工具
2. 2013年流行的[bower](https://bower.io/)（官网已经建议使用yarn了）
3. 2015年流行的npm
4. 2016年有流行苗头的yarn，但现在用npm的还是比较多
5. npm原本是为node设计的，因此，对于要在浏览器js，用npm管理是非常奇怪的选择，但可以通过npm下载包，然后再node_modules中查找min.js
6. 但这就会有个问题，在node_modules找具体是js很费劲，其次，还需要手工插入到html页面中

## 模块绑定器webpack

1. js开始设计是在浏览器运行的，故不允许跨文件导入导出代码，因为读取客户端电脑是不安全的
2. 不允许导入导出，就只能将全部代码放在全局变量上，一个页面无论你是否使用，都会被引入
3. 2009，CommonJS项目解决了这个问题，node是CommongJS的最佳实现，故node解决了上述npm的问题，无需手动插入js到页面，node可以访问文件系统，故知道node_moddules的位置
4. 但浏览器不能访问文件系统，加载模块并不仅仅是同步或异步，而是复杂的动态过程
5. 模块绑定器的作用就是绕过浏览器与访问文件系统，将require全部替换为实际内容，输出一个捆绑好的js
6. 2011，browserify让浏览器可以使用require
7. 2015，由于react的推动，webpack火起来

## 编译语言新特性（babel）

1. 比如一些新的语言特性，浏览器并不支持，可以使用babel进行转义
2. 但是通过wepack合并的文件可能会比较大，故需要进行压缩，优化图片等，需要使用时npm scripts

## 使用npm scripts

1. 2013年，Grunt、Gulp非常流行，他们都是依赖于对命令行的包装
2. 现在利用npm内置的执行脚本能力

## 结论

1. 越来越多的软件提供cli构建项目，让写代码更容易