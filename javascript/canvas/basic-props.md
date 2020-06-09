# Canvas 基本属性

### 基本介绍
如何在页面上显示canvas    
```html
    <canvas width="300" height="300"></canvas>
    <canvas style="width:300px;height:300px"></canvas>
```
上述两种方法都会在页面上显示300\*300的画布，width和height写在canvas属性上，会实际体现到绘图的宽高，写在style上仅仅体现页面的宽高。    
下面就表示绘图区域为(0,0)~(300, 300),实际显示在页面上的大小为100\*100，    
*此方法通常用于移动端的高清绘图，获取设备的devicePixelRatio，设置对应的放大倍数*
```html
    <canvas width="300" heigth="300" style="width:100px;heigth:100px"></canvas>
```

### 示例
下图表示在绘图区绘制一个300\*300的红色矩形，实际显示在页面上的尺寸为300/dpr + 'px'(*iphoneXS为3倍屏,100px*)
```html
    <canvas id="myCanvas"></canvas>
    <script>
        var dpr = window.devicePixelRatio;
        var WIDTH = 300;
        var HEIGHT = 300;
        myCanvas.width = dpr * WIDTH;
        myCanvas.heigth = dpr * HEIGHT;
        myCanvas.style.width = WIDTH + 'px'
        myCanvas.style.height = HEIGHT + 'px';
        var cxt = myCanvas.getContext("2d");
        cxt.fillStyle="#FF0000";
        cxt.fillRect(0, 0, WIDTH, HEIGHT);
    </script>
```

### 其他情况
部分游戏，不同手机拥有不同大小的屏幕，为保证公平，让所有的设备绘图区域相同，可能会采用如下方法：
```html
    <canvas id="myCanvas"></canvas>

    <script>
        var WIDTH = 750;
        var HEIGHT = 1500;
        myCanvas.width = WIDTH;
        myCanvas.height = HEIGHT;
        myCanvas.style.width = window.innerWidth + 'px';
        myCanvas.style.height = window.innerHeight + 'px';
        // 这样做保证了所有的手机地图大小都是700*1500
        // 缺点是手机横向清晰度和纵像清晰度不一致
    </script>
```

### 常用属性
```
    ctx.fillStyle = 'red' // 设置填充颜色
    ctx.strokeStyle = 'red' // 设置笔触颜色
    ctx.lineWidth = '5' // 设置线条宽度
    ctx.lineCap = 'round' // 设置线条样式 butt/round/square
    ctx.lineJoin = 'round' // 两条线条的连接类型 bevel/round/miter
    ctx.miterLimit = 5 // 设置最大斜角长度(两条线交汇处内角和外角之间的距离)
```