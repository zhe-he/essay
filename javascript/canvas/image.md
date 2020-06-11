# Canvas 图像处理
由于canvas是画布，我们可以获取指定区域的像素数据，对其进行任何形式加工处理

```html
    <canvas id="myCanvas" width="300" height="300"></canvas>
    <script>
        var ctx = myCanvas.getContext("2d");
        var image = new Image();
        image.onload = function () {
            ctx.drawImage(image, 0, 0, 300, 300);
        }
        image.onerror = function () {
            this.onerror = null;
            this.onload = null;
        }
        image.src = "./tmp.png";
        
    </script>
```

### 颜色反转
```javascript
    var imgData = ctx.getImageData(0, 0, 300, 300);
    for(var i = 0; i < imgData.data.length; i+=4) {
        // 一个像素点有4个入口 red, green, blue, alpha
        imgData.data[4 * i] = 255 - imgData.data[4 * i];
        imgData.data[4 * i + 1] = 255 - imgData.data[4 * i + 1];
        imgData.data[4 * i + 2] = 255 - imgData.data[4 * i + 2];
    }
    ctx.putImageData(imgData, 0, 0);
```

### 左右翻转
```javascript
    var imgData = ctx.getImageData(0, 0, 300, 300);
    var imgDataCopy = ctx.getImageData(0, 0, 300, 300);
    var height = imgData.height;
    var width = imgData.width;
    for(var i = 0; i < height; i++) {
        for(var j = 0; j < width; j++) {
            imgData[(i * width + j) * 4] = imgDataCopy[(i * width + width - 1 - j) * 4];
            imgData[(i * width + j) * 4 + 1] = imgDataCopy[(i * width + width - 1 - j) * 4 + 1];
            imgData[(i * width + j) * 4 + 2] = imgDataCopy[(i * width + width - 1 - j) * 4 + 2];
        }
    }
```
左右翻转优化(循环到中间即可)
```javascript
    var imgData = ctx.getImageData(0, 0, 300, 300);
    var height = imgData.height;
    var width = imgData.width;
    for(var i = 0; i < height; i++) {
        for(var j = 0; j < width/2; j++) {
            exchange(imgData[(i * width + j) * 4], imgData[(i * width + width - 1 - j) * 4]);
            exchange(imgData[(i * width + j) * 4 + 1], imgData[(i * width + width - 1 - j) * 4 + 1]);
            exchange(imgData[(i * width + j) * 4 + 2], imgData[(i * width + width - 1 - j) * 4 + 2]);
        }
    }
    // 互换
    function exchange(a, b) {
        [b, a] = [a, b];
    }
```

### 其他
所有的图像操作，都是操作具体像素点
