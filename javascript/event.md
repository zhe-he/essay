# 事件委托(事件代理)
利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。    

### 示例
点击li，弹出对应的索引
```html
    <ul id="box"></ul>

    <script>
        for(var i = 0; i < 10; i++) {
            box.innerHTML += '<li>' + (i + 1) + '</li>';
        }
        box.onclick = function (ev) {
            // 获取鼠标实际点击的目标元素
            var target = ev.target;
            // 判断是否点击的是li标签
            if (target.tagName == "LI") {
                alert("点击了第" + target.innerHTML + "个li标签")
            }
        }
    </script>
```
### 复杂场景
1. 点击li标签进入详情页面
2. 点击div.del删除这一行内容
```html
    <ul id="box">
        <li class="detail">
            <p>内容介绍</p>
            <div class="del">
                <i><!--删除图标--></i>
                <span>删除</span>
            </div>
        </li>
    </ul>
    <script>
        box.addEventListener('click', function (ev) {
            var target = ev.target;
            while(target && target.className != 'del') {
                target = target.parentNode;
            }
            // 经过上面的循环，target只有2个结果: undefined 和 div.del
            // undefined的来由：循环递进到window，window.parentNode == undefined
            
            // 点击到了 div.del 里面的元素(含自己)
            if (target == 'del') {
                target.parentNode.remove();
                ev.stopPropagation(); // 阻止事件传播
            }
        }, false)
        box.addEventListener('click', function (ev) {
            var target = ev.target;
            while(target && target.className != 'detail') {
                target = target.parentNode;
            }
            if (target == 'detail') {
                window.location.href = "详情页.html"
            }
        }, false)
    </script>
```

### 优化
虽然上述通过ev.stopPropagation阻止删除的事件传播防止触发跳转详情的事件，但上述代码可以写在一块。    
```javascript
    box.addEventListener('click', function (ev) {
        var target = ev.target;
        var classList = ['del', 'detail'];
        while(target) {
            if (classList.includes(target.className)) {
                break;
            }
            target = target.parentNode;
        }
        if (target != undefined) {
            if (target.className === 'del') {
                target.parentNode.remove();
            } else if (target.className === 'detail') {
                window.location.href = "详情页.html";
            }
        }
    }, false);
```
