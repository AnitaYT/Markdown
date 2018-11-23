## mocha 
### JavaScript测试框架,主要用来运行测试脚本

参考文档：
[阮一峰参考文档](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)

对xxx.vue进行测试, 我们就要写测试脚本, 通常测试脚本应该与Vue组件名相同,后缀为spec.js。 比如, Counter.vue组件的测试脚本名字就应该为Counter.spec.js
实例：
Counter.vue
```
//Counter.vue

<template>
  <div>
    <h3>Counter.vue</h3>
    {{ count }}
    <button @click="increment">自增</button>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        count: 0
      }
    },

    methods: {
      increment () {
        this.count++
      }
    }
  }
</script>
```

Counter.spec.js
```
//Counter.spec.js

import Vue from 'vue'
import Counter from '@/components/Counter'

describe('Counter.vue', () => {   // describe：测试套件(test suite),类型是fuction, 表示一组相关的测试。param1:套件名称，通常是测试组件名称;params2:实际执行函数

  it('点击按钮后, count的值应该为1', () => {   
    // it：测试用例(test case),类型是fuction,表示一个单独的测试, 是测试的最小单位.param1:测试用例名称，通常是描述断言结果;params2:实际执行函数
    //获取组件实例
    const Constructor = Vue.extend(Counter);
    //挂载组件
    const vm = new Constructor().$mount();
    //获取button
    const button = vm.$el.querySelector('button');
    //新建点击事件
    const clickEvent = new window.Event('click');
    //触发点击事件
    button.dispatchEvent(clickEvent);
    //监听点击事件
    vm._watcher.run();
    // 断言:count的值应该是数字1
    expect(Number(vm.$el.querySelector('.num').textContent)).to.equal(1);
    // done() Mocha中的异步测试, 需要给it()内函数的参数中添加一个done
  })
})
 // mocha测试钩子:
describe('钩子说明', function() {

  before(function() {
    // 在本区块的所有测试用例之前执行
  });

  after(function() {
    // 在本区块的所有测试用例之后执行
  });

  beforeEach(function() {
    // 在本区块的每个测试用例之前执行
  });

  afterEach(function() {
    // 在本区块的每个测试用例之后执行
  });

});
```
一个测试脚本应该包含一个或多个describe, 每个describe块应该包括一个或多个it块。


