vue单元测试

# 一.创建新项目
创建项目
```
# 使用脚手架初始化vue项目
vue init webpack

注意下面这些，其它都是直接回车为默认

# Use ESLint to lint your code? 选择 n

# Pick a test runner 选择 Karma and Mocha

# Should we run `npm install` for you after the project has been created? 在创建完项目后是否直接npm install
选择 No, I will handle that myself
因为我们已经安装了淘宝镜像，选择自己安装
```
安装与配置
进入项目安装依赖

```
cnpm install    
```                                                                                                                                                               


修改package.json,auto-watch自动监测测试文件内容修改,调试单元测试时使用

```
"debug": "cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --auto-watch",
"unit": "cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --single-run",
"test": "npm run debug",
```

安装vue-test-utils
```
cnpm install --save-dev vue-test-utils
```
测试准则
你测试的是什么？

它是做什么的？

它实际输出了什么（实际行为）？

它本该输出什么（预期的行为）？

使用
运行命令
```
#启动本地服务
npm run dev                                                    

# 单元测试
npm run test    调试测试案例时使用，监听文件改变。文件一改变，重新测试
npm run unit    一次性打出测试案例bug与结果，并终止命令	

# build
npm run build
```

框架
Karma + Mocha + chai + vue-test-utils

Karma
google的一套前端测试运行框架,用于启动一个web服务，运行测试案例并将结果报告给我们。主要作用是将项目运行在各种主流Web浏览器进行测试。

文档: https://karma-runner.github.io/

Mocha
一个测试框架。

英文文档：https://mochajs.org/

中文文档：https://www.jianshu.com/p/9c78548caffa

阮一峰：http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html

chai
一个测试断言库。就是对组件做一些操作，并预言产生的结果。如果测试结果与断言相同则测试通过。Chai断言库中，to be been is that which and has have with at of same but does这些语言链是没有意义的，只是便于理解。

英文文档：http://www.chaijs.com/api/bdd/

翻译版：https://www.jianshu.com/p/f200a75a15d2

Vue Test Utils
Vue Test Utils 是 Vue.js 官方的单元测试实用工具库。

官方文档: https://vue-test-utils.vuejs.org/zh/

api：https://vue-test-utils.vuejs.org/zh/api/wrapper/

案例
案例一
test/unit/specs/HelloWorld.spec.js

```
import Vue from 'vue' // 导入Vue用于生成Vue实例
import HelloWorld from '@/components/HelloWorld' // 导入组件

// 测试脚本里面应该包括一个或多个describe块，称为测试套件（test suite）
describe('HelloWorld.vue', () => {
  // 每个describe块应该包括一个或多个it块，称为测试用例（test case）
  it('should render correct contents', () => {
    const Constructor = Vue.extend(HelloWorld) // 获得HelloWorld组件实例
    const vm = new Constructor().$mount() // 将组件挂在到DOM上	
	// 断言：DOM中class为hello的元素中的h1元素的文本内容为[Welcome to Your Vue.js App]
    expect(vm.$el.querySelector('.hello h1').textContent)
      .to.equal('Welcome to Your Vue.js App')
  })
})
```
我们在HelloWorld.spec.js引入vue-unit-test，简化写法

测试结果正确，返回以下
```
 HelloWorld.vue
    ✓ 检测h1的内容
Chrome 69.0.3497 (Mac OS X 10.13.4): Executed 1 of 1 SUCCESS (0.012 secs / 0.002 secs)
TOTAL: 1 SUCCESS

=============================== Coverage summary ===============================
Statements   : 66.67% ( 2/3 )
Branches     : 100% ( 0/0 )
Functions    : 100% ( 0/0 )
Lines        : 66.67% ( 2/3 )
================================================================================
```
Coverage summary
Statements: 声明（是否每个语句都执行了？）

Branches: 分支（是否每一个if都执行了？）

Functions: 函数（是否每一个函数都调用了？）

Lines: 行（是否每一行都执行了？）



当运行结果出来后，打开test/unit/coverage/lcov-report/index.html

html里可以比较直观的看出每一块的覆盖率



如果我们把断言里的实际结果改一下
```
expect(hello.text()).to.equal('hahahaha');
```
测试结果错误，返回以下。

检测h1的内容报错，期望是「Welcome to Your Vue.js App」，实际却是「hahahaha」
```
 HelloWorld.vue
    ✗ 检测h1的内容
        AssertionError: expected 'Welcome to Your Vue.js App' to equal 'hahahaha'
            at Context.<anonymous> (webpack:///test/unit/specs/HelloWorld.spec.js:10:28 <- index.js:11897:29)

Chrome 69.0.3497 (Mac OS X 10.13.4): Executed 1 of 1 (1 FAILED) ERROR (0.075 secs / 0.002 secs)

=============================== Coverage summary ===============================
Statements   : 66.67% ( 2/3 )
Branches     : 100% ( 0/0 )
Functions    : 100% ( 0/0 )
Lines        : 66.67% ( 2/3 )
================================================================================
```

案例二
修改一下HelloWorld.vue,我们加一个h2,h2值默认为1，增加一个点击事件，点击后h2的值+1

点击一次为 2

再点击一次为 3

再点击一次为 4
```
<h2 @click="changeText">{count}</h1>
```
```
methods: {
  data() {
    count: 1
  },
  changeText() {
    this.count++
  }
}
```

现在我们测试这个方法
```
import HelloWorld from '@/components/HelloWorld'
import {mount} from 'vue-test-utils';
const wrap = mount(HelloWorld);
const vm = wrap.vm;

describe('HelloWorld.vue', () => {

  it('h2点击事件', () => {
    let countDom = wrap.find('.hello h2'); // h2
    let count = vm.count; // h2绑定的count

    countDom.trigger('click'); // 点击h2

    let countAfterClick = vm.count; // 获取点击后的count

	// 断言：点击后的count的值为之前值 +1
    expect(countAfterClick).to.equal(count + 1)

  })
});
```

测试结果
```
 HelloWorld.vue
    ✓ h2点击一次，值+1
Chrome 69.0.3497 (Mac OS X 10.13.4): Executed 1 of 1 SUCCESS (0.016 secs / 0.009 secs)
TOTAL: 1 SUCCESS

=============================== Coverage summary ===============================
Statements   : 100% ( 3/3 )
Branches     : 100% ( 0/0 )
Functions    : 100% ( 0/0 )
Lines        : 100% ( 3/3 )
================================================================================
```
注意
测试脚本都要放在 test/unit/specs/ 目录下。

脚本命名方式为 [组件名].spec.js。

测试脚本由多个 descibe 组成，每个 describe 由多个 it 组成。

Demo地址
git@code.xiaomai9.com:xmfe/template.git（xmts）

# 二.已有项目安装测试环境
安装依赖
package.json 增加
```
"vue-test-utils": "^1.0.0-beta.11",
"sinon": "^4.0.0", //测试辅助工具，提供 spy、stub、mock 三种测试手段，帮助捏造特定场景
"sinon-chai": "^2.8.0", //karma 中的 chai 插件
"karma": "^1.4.1",
"karma-chrome-launcher": "^2.2.0",
"karma-coverage": "^1.1.1",
"karma-junit-reporter": "^1.2.0",
"karma-mocha": "^1.3.0",
"karma-phantomjs-launcher": "^1.0.2",
"karma-phantomjs-shim": "^1.4.0",
"karma-sinon-chai": "^1.3.1",
"karma-sourcemap-loader": "^0.3.7",
"karma-spec-reporter": "0.0.31",
"karma-webpack": "^2.0.2",
"mocha": "^3.2.0",
"chai": "^4.1.2",
"cross-env": "^5.0.1",
"karma-junit-reporter": “^1.2.0",
"babel-polyfill": "^6.26.0",  // phantom 兼容ES6 promise
```

修改配置
package.json 修改

```
"scripts": {
  "debug": "cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --auto-watch",
  "unit": "cross-env BABEL_ENV=test karma start test/unit/karma.conf.js --single-run",
  "test": "npm run debug",
},
```

.babelrc（不修改这个造成覆盖率为0）

```
 "plugins": ["transform-vue-jsx", "istanbul"]
```
配置 karma
在项目根目录新建一个文件夹test/unit，进入到unit，执行命令
```
karma init
```

```
Which testing framework do you want to use ?
选择mocha 
```
先后选择使用的测试框架、是否使用 require.js、浏览器环境、测试脚本存放位置等等。除了第一个选择mocha框架，其它都默认，回车。选择完毕之后，在unit下生成一个 karma.conf.js 文件

karma插件配置
```
// karma.conf.js
// This is a karma config file. For more details see
//   http://karma-runner.github.io/0.13/config/configuration-file.html
// we are also using it with karma-webpack
//   https://github.com/webpack/karma-webpack
var webpackConfig = require('../../build/webpack.test.conf')
module.exports = function karmaConfig (config) {
  config.set({
    // 测试所用平台
    browsers: ['PhantomJS'],
    // 使用的测试框架
    frameworks: ['mocha', 'sinon-chai', 'phantomjs-shim'],
    // 测试日志格式
    reporters: ['spec', 'coverage', 'junit'],
    files: ['../../node_modules/babel-polyfill/dist/polyfill.js',
      './index.js'
    ],
    preprocessors: {
      './index.js': ['webpack', 'sourcemap']
    },
    // `webpack` 配置
    webpack: webpackConfig,
    webpackMiddleware: {
      noInfo: true
    },
    // 代码覆盖率日志
    coverageReporter: {
      dir: './coverage',
      reporters: [
        { type: 'lcov', subdir: '.' },
        { type: 'text-summary' }
      ]
    },
    junitReporter: {
      outputDir: './coverage',
      outputFile: 'coverage.xml',
      useBrowserName: false
    }
  })
};
```

在test/unit/新建一个index.js

```
import Vue from 'vue'
Vue.config.productionTip = false
// require all test files (files that ends with .spec.js)
const testsContext = require.context('./specs', true, /\.spec$/)
testsContext.keys().forEach(testsContext)
// require all src files except main.js for coverage.
// you can also change this to match only the subset of files that
// you want coverage for.
const srcContext = require.context('../../src', true, /^\.\/(?!main(\.js)?$)/)
srcContext.keys().forEach(srcContext)
```

在build文件里新建webpack.test.conf.js
```
// webpack.test.conf.js
'use strict'
// This is the webpack config used for unit tests.
const utils = require('./utils')
const webpack = require('webpack')
const merge = require('webpack-merge')
const baseWebpackConfig = require('./webpack.base.conf')
const webpackConfig = merge(baseWebpackConfig, {
  // use inline sourcemap for karma-sourcemap-loader
  module: {
    rules: utils.styleLoaders()
  },
  devtool: '#inline-source-map',
  resolveLoader: {
    alias: {
      // necessary to to make lang="scss" work in test when using vue-loader's ?inject option
      // see discussion at https://github.com/vuejs/vue-loader/issues/724
      'scss-loader': 'sass-loader'
    }
  },
  plugins: [
    new webpack.DefinePlugin({
      'process.env': require('../config/test.env')
    })
  ]
})
// no need for app entry during tests
delete webpackConfig.entry
module.exports = webpackConfig		
```
以上都配置好了，框架搭建完成。

第一个测试用例
在src/components 新建一个HelloWorld
```
 <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2 @click="changeText">{{count}}</h2>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      count: 1
    }
  },
  methods: {
    changeText() {
      this.count++
    }
  }
}
</script>
```

在test/unit/specs 里新建一个HelloWorld.spec.js
```
 import HelloWorld from '@/components/HelloWorld'
import {mount} from 'vue-test-utils';
const wrap = mount(HelloWorld);
const vm = wrap.vm;
describe('HelloWorld.vue', () => {
  it('检测h1的内容', () => {
    let hello = wrap.find('.hello h1');
    expect(hello.text()).to.equal('Welcome to Your Vue.js App')
  });
  it('h2点击一次，值+1', () => {
    let countDom = wrap.find('.hello h2'); // h2
    let count = vm.count; // h2绑定的count
    countDom.trigger('click'); // 点击h2
    let countAfterClick = vm.count; // 获取点击后的count
    // 断言：点击后的count的值为之前值 +1
    expect(countAfterClick).to.equal(count + 1)
  })
});
```

启动test命令
```
npm run test 
```


显示结果
```
 HelloWorld.vue
   ✓ 检测h1的内容
   ✓ h2点击一次，值+1
Chrome 69.0.3497 (Mac OS X 10.13.4): Executed 2 of 2 SUCCESS (0.02 secs / 0.006 secs)
TOTAL: 2 SUCCESS

=============================== Coverage summary ===============================
Statements   : 100% ( 0/0 )
Branches     : 100% ( 0/0 )
Functions    : 100% ( 0/0 )
Lines        : 100% ( 0/0 )
================================================================================
```


* 测试脚本都要放在 test/unit/specs/ 目录下。 
* 脚本命名方式为 [组件名].spec.js。 
* 所谓断言，就是对组件做一些操作，并预言产生的结果。如果测试结果与断言相同则测试通过。 
* 单元测试默认测试 src 目录下除了 main.js 之外的所有文件，可在 test/unit/index.js 文件中修改。 
* Chai断言库中，to be been is that which and has have with at of same 这些语言链是没有意义的，只是便于理解而已。 
* 测试脚本由多个 descibe 组成，每个 describe 由多个 it 组成。 
* 了解异步测试
