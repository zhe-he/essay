# rem布局
rem是相对根元素html的font-size来决定大小的，我们可以通过js脚本来改变根元素的font-size来实现自适应，一般使用在手机端。    
其他：em是相对父元素的font-size来决定大小    

#### 例子
```html
    <html>
        <head>
            <style>
                html{font-size: 10px;}
                .main{font-size: 30rem;height: 10rem;}
            </style>
        </head>
        <body>
            <div class="main"><div>
            <script>
                // 判断手机是否支持横竖屏事件，如果不支持降纬使用resize事件
                var orientation = "onorientationchange" in window ? "orientationchange" : "resize";
                var isIos = /(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent);
                var timer = window.addEventListener(orientation, fn, false);
                fn();
                function fn() {
                    // 因为ios手机横竖屏会实时响应，而不少安卓手机响应横竖屏会延迟
                    // 判断是否为ios，如果不是ios，开启定时器延迟执行
                    // 防止用户频繁转动手机，清空上次的定时器
                    clearTimeout(timer);
                    timer = setTimeout(function () {
                        // 设计图尺寸750px对应基准10px
                        var size = Math.round(window.innerWidth / 750 * 10);
                        // 设置基准
                        document.documentElement.style.fontSize = size + 'px';
                    }, isIos ? 0 : 30);
                }
            </script>
        </body>
    </html>
```