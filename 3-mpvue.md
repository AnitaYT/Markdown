[mpvue详细讲解](https://www.jianshu.com/p/6f8d74be3ff8)

### mpvue 目录结构

### 使用步骤

- 1. vue init mpvue/mpvue-quickstart xxx(项目目录)
- 2. cd firstapp 
- 3. npm install
- 4. npm run dev

成功运行后,项目代码就进入开发模式，一旦有源代码发生修改，就会触发自动编译。
因为mpvue使用的是Vue + HTML Web的开发方式开发小程序，它最终需要被转换成小程序的代码才可以在小程序环境运行，所以这里的自动编译的目的就是要把Web代码编译成小程序代码。编译后的代码会在dist目录下。

- 5. 使用微信开发工具打开dist目录

### 说明
main.js + App.vue：这两个是入口文件，相当于原生小程序框架中的app.json和app.js的复合体。
## 开始使用
Vue组件App.vue 实现与微信小程序app.js的等价功能。在这个组件中可以编写
小程序的生命周期方法(script标签内)，也可以加入小程序的全局样式（style标签内）（等价于原生方式下的app.wxss）
**src/App.vue**

```
<script>
  /* 这部分相当于原生小程序的 app.js */
  export default {}
</script>

<style>
  /* 这部分相当于原生小程序的 app.wxss */
</style>
```
**src/main.js**
```
import Vue from 'vue'
import App from './App'

Vue.config.productionTip = false
/* App.mpType = 'app';
这个值是为了与后面要讲的小程序页面组件所区分开来，因为小程序页面组件和这个App.vue组件的写法
和引入方式是一致的，为了区分两者，需要设置mpType值。引入这个App.vue组件后
会用它作为参数来创建一个Vue的实例，并调用$mount()方法加载。
 */
App.mpType = 'app'

const app = new Vue(App)
app.$mount()

export default {
  // 这个字段走 app.json / 这部分相当于原生小程序的 app.json
  config: {
    // 页面前带有 ^ 符号的，会被编译成首页，其他页面可以选填，我们会自动把 webpack entry 里面的入口页面加进去
    pages: ['pages/logs/main', '^pages/index/main'],
    window: {
      backgroundTextStyle: 'light',
      navigationBarBackgroundColor: '#fff',
      navigationBarTitleText: '使用mpvue的小程序',
      navigationBarTextStyle: 'black'
    }
  }
}
```
*tip:*

在src/page下每次新建一个页面都要有一个子目录（请遵循每个页面放入一个子目录的良好习惯）。然后在该子目录下，新建2个文件：一个用于实现页面主体功能的.vue组件，另一个则用于将这个页面组件生成Vue实例并加载的.js文件。
```
|-- src     
    |-- pages     页面资源目录
        |-- home    home页面
            |-- home.vue
            |-- main.js
            |-- store.js  状态管理文件
        |-- finding    finding页面
            |-- finding.vue
            |-- main.js
        ...
```
**pages/home** 引入home组件并做一些单独的配置
```
import Vue from 'vue'       // 引入vue
import App from './index'   //引入组件

const app = new Vue(App)    // 创建实例
app.$mount()                // 挂载实例

export default {
  config: {
    // 设置页面的title 
    // 注意，页面级可配置属性相当于只是`src/main.js`中配置里的`window`部分
    "navigationBarTitleText": "xxx"
  }
}
```
原生小程序的页面（Page）中包含了很多页面的生命周期方法，如onLoad、onUnload、onShow、onHide、onPullDownRefresh等等，mpvue中推荐使用Vue组件生命周期方法，而像onPullDownRefresh、onReachBottom这类特殊功能的生命周期则需直接使用原生的。

**小程序优秀的UI组件库**
```
1.
WeUI WXSS
WeUI WXSS是腾讯官方UI组件库WeUI的小程序版，提供了跟微信界面风格一致的用户体验。
GitHub地址：https://github.com/Tencent/weui-wxss
npm下载：npm i weui-wxss

2.
iView WeApp
iView是TalkingData发布的一款高质量的基于Vue.js组件库，而iView weapp则是它们的小程序版本。

GitHub地址：https://github.com/TalkingData/iview-weapp
npm下载：npm i iview-weapp

3.
ZanUI WeApp
ZanUI WeApp是有赞移动 Web UI 规范 ZanUI 的小程序实现版本，结合了微信的视觉规范，为用户提供更加统一的使用感受。

现已包含 badge、btn、card、cell、dialog、icon、label、noticebar、panel、popup、switch、tab、toast、tooltips 等组件或元素。

GitHub地址：https://github.com/youzan/zanui-weapp
npm下载：npm i zanui-weapp

另外，ZanUI也使用mpvue重写了zanui-weapp，实现了其中所有组件，为使用mpvue的开发者提供了方便。

GitHub地址：https://github.com/samwang1027/mpvue-zanui
npm下载：npm i mpvue-zanui

4.
MinUI
MinUI 是蘑菇街前端开发团队开发的基于微信小程序自定义组件特性开发而成的一套简洁、易用、高效的组件库，适用场景广，覆盖小程序原生框架，各种小程序组件主流框架等，并且提供了专门的命令行工具。

GitHub地址：https://github.com/meili/minui

5.
Wux WeApp
Wux WeApp也是一个非常不错的微信小程序自定义 UI 组件库，组件比较丰富，值得使用。

GitHub地址：https://github.com/wux-weapp/wux-weapp
npm下载：npm i wux-weapp
```

