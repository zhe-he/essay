# 冒泡排序
![冒泡排序](../source/images/algorithm/bubble.gif)

### 定义
依次比较两个相邻的元素，如果顺序错误就把他们交换过来。走访元素的工作是重复地进行直到没有相邻元素需要交换，也就是说该元素列已经排序完成。

### 思路
1. 我们先循环整个数组两两比较一次<从左至右>
1. 执行上一步后，最后一个元素为排列好的元素，接着循环数组(不包含排列好的元素)
1. 直到所有的元素排列好为止

### 代码
1. 第一步:  
```
    var arr = [9, 5, 6, 8, 2, 7, 3, 4, 1];
    for（var i = 0; i < arr.length; i++) {
        if(arr[i] > arr[i + 1]) {
            // 交换位置
            [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
        }
    }
```
1. 第二步:
```
    /**
     * 用一个变量记录需要排序的个数
     * 每次排序后，变量值-1
     * 直到变量值为0为止
     */
    var arr = [9, 5, 6, 8, 2, 7, 3, 4, 1];
    var n = arr.length;
    while (n > 0) {
        for（var i = 0; i < n; i++) {
            if(arr[i] > arr[i + 1]) {
                // 交换位置
                [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
            }
        }
        n--;
    }
```
1. 封装:
```
    function bubbleSort(arr) {
        var n = arr.length;
        while (n > 0) {
            for（var i = 0; i < n; i++) {
                if(arr[i] > arr[i + 1]) {
                    // 交换位置
                    [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
                }
            }
            n--;
        }
        return arr;
    }

    // 调用
    var arr = [9, 5, 6, 8, 2, 7, 3, 4, 1];
    bubbleSort(arr);
```
1. 优化:
    * 数组循环到最后一个时，i+1已越界，需要做边界处理
    * n为1时，不需要比较(在上一次n=2时,已经比较完成)
```
    function bubbleSort(arr) {
        var n = arr.length;
        while(n > 1) {
            for（var i = 0; i < n - 1; i++) {
                if(arr[i] > arr[i + 1]) {
                    // 交换位置
                    [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
                }
            }
            n--;
        }
        return arr;
    }
```

### 练习
感兴趣的小伙伴可以写一个从大到小的排序，循环数组时从右往左
```
    // 模版
    for(var i = arr.length - 1; i >= 0 ; i++) {
    }
```
