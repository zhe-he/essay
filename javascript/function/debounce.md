# 函数防抖
事件被触发后n秒才执行的函数

### 简易版本
```
    function debounce(func, wait) {
        var timer = null;
        return function () {
            clearTimeout(timer);
            timer = setTimeout(function () {
                func();
            }, wait);
        }
    }

    var t = debounce(function() {
        console.log(123);
    }, 1000);
    // 只会打印一个123，一秒后才执行
    t();
    t();
```

### 完整版本
1. 部分函数会有形参
1. 部分场景需要立即执行
```
    function debounce(func, wait, immediate) {
        var timer = null;
        return function () {
            clearTimeout(timer);
            var that = this;
            var args = arguments;
            if (immediate && !timer) {
                func.apply(that, args);
            }
            timer = setTimeout(function () {
                if (!immediate) {
                    func.apply(that, args);
                }
            }, wait);
        }
    }
    var t = debounce(function() {
        console.log(123);
    }, 1000, true);
    // 只会打印一个123，立即执行
    t();
    t();
```

### 简化版本
利用es6简化this和arguments
```
    function debounce(func, wait, immediate) {
        var timer = null;
        return function (...args) {
            clearTimeout(timer);
            if (immediate && !timer) {
                func.apply(this, args);
            }
            timer = setTimeout(() => {
                if (!immediate) {
                    func.apply(this, args);
                }
            }, wait);
        }
    }
```

### 应用场景
1. 联想搜索，用户在不断输入值时，一段时间内只查询最后一次输入减少请求。
1. resize事件，一段时间内只触发最后一次resize事件。
