# 过渡transition
过渡需要触发一个事件才会随着时间改变其CSS属性，他是一个复合属性。    

|属性名|说明|
|:---|:---|
|transiton|*property duration timing-function delay*|
|transition-property|需要过渡的属性(默认值为all)|
|transition-duration|过渡持续时间(默认值为0s)|
|transiton-timing-function|过渡函数(默认值为ease函数)|
|transition-delay|过渡延迟时间(默认值为0s)|

### 示例
```html
    <style>
        .box{ width: 100px; height: 100px; background: red; transition: all 1s linear 0.2s; }
        .box:hover{ width: 200px; }
    </style>
    <!--当鼠标移入div时宽度会延迟0.2s后线性过渡1秒达到200px-->
    <div class="box"></div>
```

### 其他
```CSS
    // 简写省略最后一个参数
    transition: all 1s linear;
    // 简写省略后两个参数
    transition: all 1s;
    // 过渡多个属性，逗号隔开
    transition: width 1s, height 0.2s;
    // 自定义过渡曲线(贝塞尔曲线)
    transition-timing-function: cubic-bezier(0.42,0,0.58,1);
```