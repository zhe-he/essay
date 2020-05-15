# 希尔排序
![希尔排序](../source/images/algorithm/shell.gif)

### 定义
把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止

### 代码
```
    function shellSort(arr) {
        var center = Math.floor(arr.length / 2);
        for (var i = center; i > 0; i = Math.floor(i / 2)) {
            for (var j = i; j < arr.length; j++) {
                for (var k = j - i; k >= 0 && arr[k] > arr[i + k]; k -= i) {
                    // 交换位置
                    [arr[k], arr[i + k]] = [arr[i + k], arr[k]]
                }
            }
        }
        return arr;
    }
```