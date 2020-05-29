# 动画animation
动画是自动自行的，需要自定义一个动画名称，他是一个复合属性。    

|属性名|说明|
|:---|:---|
|animation|*name duration timing-function delay iteration-count direction*|
|animation-name|动画名称|
|animation-duration|过渡持续时间|
|animation-timing-function|ease &#124; linear &#124; ease-in &#124; ease-out &#124; ease-in-out &#124; cubic-bezier(n, n, n, n)|
|animation-delay|过渡延迟时间|
|animation-iteration-count|动画循环的次数(默认1)|
|animation-direction|动画播放的方向(normal &#124; alternate)|
|animation-play-state|动画的播放状态(running &#124; paused)|

### 示例
```html
    <style>
        .box {
            position: absolute;
            top: 0;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: red;
            animation: move 1s ease infinite;
        }
        /* 0%可以写成from，100%可以写成to */
        @keyframes move{
            0%{ left: 0 }
            100%{ left: 200px; }
        }
    </style>
    <!--box无限次执行1s的动画move-->
    <div class="box"></div>
```
```CSS
    /* 如果给上面的动画添加一个属性 */
    /* box先从左运动到右，再从右运动到左，再从左运动到右... */
    animation-direction: alternate;

    /* 如果给box添加如下的hover事件 */
    /* box会在鼠标移入的时候暂停动画 */
    .box:hover{ animation-play-state: paused; }

    /* 添加多个动画，逗号隔开 */
    animation: move 1s ease infinite, move2 1s;
```
