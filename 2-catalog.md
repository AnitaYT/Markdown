###  前端目录结构

```
|-- 项目名
    index.html    静态页面模板
    login.html
    news.html
    |-- static    引用目录
        |-- font    字体目录（假设有的话）
        |-- css     样式目录
        |-- js      脚本目录
            |-- lib 基础库
                |-- jquery.min.js
                |-- and etc...
            |-- main.js
            |-- index.js
        |-- images  图片目录
            |-- project1 子项目
                |-- logo.png
                |-- bg.png
                |-- and etc...
            |-- project2 子项目
                |-- logo.png
                |-- bg.png
                |-- and etc...
            |-- and etc...
        |-- demo  示例图片目录（用于生成环境展示案例）
            |-- demo_1.jpg
            |-- demo_2.jpg
            |-- and etc...

```

### 以vue项目为例的目录结构
```
|-- project_name
    |--build      构建脚本目录
       |--webpack.dev.conf.js    配置浏览器服务脚本文件
       |--webpack.base.conf.js   vue开发环境的wepack相关配置文件，主要                           用来处理各种文件的配置
       |--utils.js            utils.js文件主要是用来处理各种css                              loader的，比如css-loader，                                    less-loader等。
       |
    config     构建配置目录
    node_modules 依赖的node工具包目录
    |-- mock    项目mock数据目录
        |-- api   mock数据目录  
            |-- home     首页mock目录
               |-- search.js
               |-- detail.js
        routes.js  mock数据 配置路由文件
        server.js  jsonServer启动文件   
    |-- src        源码目录
        |-- assets     资源目录
        |-- components 组件目录
        |-- router     路由文件资源目录
        |-- store      vue状态管理文件
           |-- home
              |-- index.js home模块的state，mutation，action
              |-- types.js home模块异步的常量定义  actionType.js 用于存放事件名称。
           |-- buy
           index.js  (new Vuex.Store)
        |-- App.vue    页面级Vue组件
        |-- main.js    页面入口js文件
    |-- static       静态文件目录
    |-- test       测试文件目录
    index.html   入口页面
    .eslinkrc.js ES语法检查配置
    package.json 项目描叙文件

```