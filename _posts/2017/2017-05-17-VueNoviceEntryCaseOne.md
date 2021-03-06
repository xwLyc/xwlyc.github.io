---
layout: post
title: "Vue新手入门案例(一)"
date: 2017-05-17
description: "Vue环境搭建以及项目结构说明"
tag: Vue 
---   
不知道大家有没有跟我一样的感受，看了很久的Vue官方文档，还是云里雾里，只知其一不知其二，不知道如何下手做一个项目。 然后开始准备写项目的时候，一看Vue的生态系统真是庞大呀，Vue-router,Vuex,webpack,es6等等，要学习的东西真的很多，一时间不知如何下手。
还好vue有款速构建项目的脚手架工具 vue-cli，当然，使用之前要把vue-cli，webpage等都安装好。具体安装说明，百度一搜一大筐。

### 项目开始
安装好vue-cli,webpack之后，使用方式如下：

 >   1. 选择简单模板搭建vue项目：vue init webpack-simple my-simple-demo
 >   2. 选择webpack（略复杂）模板搭建vue项目: vue init webpack my-webpack-demo（my-webpack-demo可以随意写）

我选择的是第二种，根据提示安装完成之后，安装过程中的 vue-router记得填写yes，会把路由依赖也安装上，根据终端的提示,

    1.cd my-webpack-demo
    2.npm install
    3.npm run dev
    4.然后会自动打开浏览器访问localhost:8080
    5.开发阶段，写你自己的项目
    6.发布阶段，发布项目  npm run build

### 项目结构

>1.目录结构 

项目流程中的第二步，npm install 之后，会在文件生成如下文件目录结构：

![a](/images/2017-05-17/a.png)

>2.目录结构介绍


| 目录/文件      | 说明           | 
| ------------- | :-------------| 
| build         | 最终发布的代码存放位置。 | 
| config        | 配置目录，包括端口号等。我们初学可以使用默认的。      |   
| node_modules  | npm 加载的项目依赖模块      |  
| src           | 这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：  <br> * assets: 放置一些图片，如logo等。  <br>    * commponents: 组件目录 <br>    * router: 路由目录。<br> * App.vue: 项目入口文件，我们也可以直接将组建写这里，而不使用 commponents 目录。<br>   * main.js: 项目的核心文件。    |  
| static  | 静态资源目录，如图片、字体等。      |    
| .xxxx文件  | 这些是一些配置文件，包括语法配置，git配置等。      |    
| index.html  | 首页入口文件，你可以添加一些 meta 信息或同统计代码啥的。      |    
| package.json  | 项目配置文件。      |    
| README.md  | 项目的说明文档，markdown 格式。      |    


>3.初始流程

#### 1.index.html ---首页入口文件
其中 id 为 app 的 div 是页面容器，渲染后的结果会挂载到这个 div 上。

        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8">
                <title>lyc</title>
            </head>
            <body>
                <div id="app"></div>
                <!-- built files will be auto injected -->
            </body>
        </html>

#### 2.main.js ----核心文件
此处的`el: '#app'`, 表示的是index中的那个 `<div id="app"></div>`, 它要被 `App` 这个组件 `components: { App }` 的模板 `template: '<App/>'`替换。 `router`，就是 `router:router`的缩写，

    // The Vue build version to load with the `import` command
    // (runtime-only or standalone) has been set in webpack.base.conf with an alias.
    import Vue from 'vue'
    import App from './App'
    import router from './router'

    Vue.config.productionTip = false

    /* eslint-disable no-new */
    new Vue({
        el: '#app',
        router,
        template: '<App/>',
        components: { App }
    })

#### 3.App.vue ----项目入口文件
App这个组件 `components: { App }` 的模板 `template: '<App/>'` 的具体内容。其中的 `router-view`会由 vue-router 去渲染组件，将结果挂载到这个 div 上

    <template>
    <div id="app">
        <img src="./assets/logo.png">
        <router-view></router-view>
    </div>
    </template>

    <script>
    export default {
        name: 'app'
    }
    </script>

    <style>
        #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
        }
    </style>

#### 4.router/index.js -----路由与组件　
引入Hello组件，将其路径对应为'/’

    import Vue from 'vue'
    import Router from 'vue-router'
    import Hello from '@/components/Hello'

    Vue.use(Router)

    export default new Router({
    routes: [
        {
        path: '/',
        name: 'Hello',
        component: Hello
        }
    ]
    })

#### 5.config/index.js -----端口配置
项目运行默认为 8080端口，如果同时运行多个本地项目会造成冲突，可更改 config/index.js下的，`dev` 对象 中的 `port` 值
