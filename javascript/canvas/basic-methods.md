# Canvas 基本方法

```html
    <canvas id="myCanvas" width="300" height="300"></canvas>
```

### 画线条
```javascript
    var ctx = myCanvas.getContext("2d");
    ctx.moveTo(50, 50); // 起点
    ctx.lineTo(100, 50);
    ctx.lineTo(100, 100);
    ctx.stroke();
```

### 画半圆
```javascript
    var ctx = myCanvas.getContext("2d");
    ctx.beginPath();
    // 圆心(100,100), 半径r50, 起点0, 终点π, 是否逆时针画图true
    ctx.arc(100, 100, 50, 0, Math.PI, true);
    ctx.closePath();
    ctx.stroke();
```
```ctx.arc(x, y, 0, Math.PI * 1.5, false) // 下图圆弧轨迹 ```    
![圆弧](../../source/images/canvas/arc.gif)


### 画渐变矩形
```javascript
    var ctx = myCanvas.getContext("2d");
    var grd = ctx.createLinearGradient(0, 0, 300, 300);
    grd.addColorStop(0, "#000000");
    grd.addColorStop(0.25, "#FF0000");
    grd.addColorStop(0.5, "#00FF00");
    grd.addColorStop(0.75, "#0000FF");
    grd.addColorStop(1, "#FFFFFF");
    ctx.fillStyle = grd;
    ctx.fillRect(0, 0, 300, 300);
```