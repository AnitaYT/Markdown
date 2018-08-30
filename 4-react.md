### 是什么？
React 是一个用于构建用户界面的 JAVASCRIPT 库。 （MVC）

### react特点
1. 声明式设计 −React采用声明范式，可以轻松描述应用。

2. 高效 −React通过对DOM的模拟，最大限度地减少与DOM的交互。

3. 灵活 −React可以与已知的库或框架很好地配合。

4. JSX − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。

5. 组件 − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。

6. 单向响应的数据流 − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。


### 使用 create-react-app 快速构建 React 开发环境
create-react-app 是来自于 Facebook，通过该命令我们无需配置就能快速构建 React 开发环境。

create-react-app 自动创建的项目是基于 Webpack + ES6 。

**步骤**
```
cnpm install -g create-react-app
create-react-app my-app
cd my-app/
npm start

如果没有装淘宝镜像：
npm install -g cnpm --registry=https://registry.npm.taobao.org
npm config set registry https://registry.npm.taobao.org

淘宝镜像安装模块
cnpm install [name]
```

### react项目目录  my-app


```
  |--node_modules/    安装的依赖
  |--public/
    |--favicon.ico
    |--index.html
    |--manifest.json
  |--src/
    |--App.css
    |--App.js
    |--App.test.js
    |--index.css
    |--index.js
    |--logo.svg
    |--registerServiceWorker.js
  README.md
  package.json
  .gitignore
```

```
manifest.json 指定了开始页面 index.html，一切的开始都从这里开始，所以这个是代码执行的源头。
```

