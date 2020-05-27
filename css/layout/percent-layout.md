# 百分比布局
通过百分比%可以实现各标签随窗口宽和高实时变化。    
需要注意的是：各个属性如果使用百分比，相对父元素的属性不一定是相对当前的属性，不一定是相对当前元素的父元素，border-radius、translate、background-size属性的百分比是相对自身的宽度。
```html
    <div class="position-parent">
        <div class="parent">
            <div class="self"></div>
        </div>
    </div>
    <style>
        .position-parent{position:relative;}
        .self{position:absolute;}
    </style>
```
|子元素属性self(%)|子元素self|父元素parent|定位的父元素position-parent|
|:---:|:---:|:---:|:---:|
|width|-|width|-|
|height|-|height|-|
|top|-|-|height|
|left|-|-|width|
|bottom|-|-|height|
|right|-|-|width|
|padding|-|width|-|
|margin|-|width|-|
|border-radius|width|-|-|
|translate|width|-|-|
|background-size|width|-|-|
