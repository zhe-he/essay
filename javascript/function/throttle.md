# 函数节流
连续触发事件但是在n秒中只执行一次的函数    

### 简易版本
```
    function throttle(func, duration) {
        setTimeout(function () {
            func();
        }, duration);
    }

    // 1秒钟后打印123
    throttle(function() {
        console.log(123);
    }, 1000);
```

### 优化版本
1. 函数下次执行，定时器需要被关闭，需要一个定时器变量。    
1. 函数执行，可能会有参数，需要一个接受函数实参的形参。 
1. 部分函数执行可能会改变this指向，需要一个改变this的形参。

```
    function throttle(func, options) {
        clearTimeout(func.timer);
        options = Object.assign({
            context: window,
            args: [],
            duration: 1000
        }, options);
        func.timer = setTimeout(function () {
            func.apply(options.context, options.args);
        }, options.duration);
    }
    function fn(a, b) {
        console.log(a, b)
    }
    // 1秒钟后打印1，2
    throttle(fn, {
        args: [1, 2]
    });

    // 如果要关闭节流函数定时器
    // clearTimeout(fn.timer);
```

### 应用场景
监听滚轮事件：滑动时判断是否显示返回顶部按钮

