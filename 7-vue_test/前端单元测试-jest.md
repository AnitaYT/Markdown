[segmentfault文章](https://segmentfault.com/a/1190000010733565)

### 优点
- 方便的异步测试
- snapshot功能
- 集成断言库，不许要引用其他第三方库
- 对React天生支持   

### 内建丰富的断言库
```
.toBe(value)
.toHaveBeenCalled()
.toBeFalsy()
.toEqual(value)
.toBeGreaterThan(number)
.toBeGreaterThanOrEqual(number)
```

### 方便的钩子
```
beforeEach（fn）
afterEach（fn)
beforeAll(fn)
afterAll(fn)
```

### 测试用例
```
import Hook from '../src/hook';

describe('hook', () => {

    const hook = new Hook;

    // 每个测试用例执行前都会还原数据，所以下面两个测试可以通过。
    beforeEach( () => {
        hook.init();
    })


    test('test hook 1', () => {
        hook.a = 2;
        hook.b = 2;
        expect(hook.sum()).toBe(4);
    })

    test('test hook 2', () => {

        expect(hook.sum()).toBe(2);// 测试通过
    })


})
```