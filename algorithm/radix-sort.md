# 基数排序
![基数排序](../source/images/algorithm/radix.gif)

### 定义
基数排序属于“分配式排序”，又称“桶子法”，顾名思义，它是透过键值的部份资讯，将要排序的元素分配至某些“桶”中，藉以达到排序的作用。

### 代码
```
    function radixSort(arr) {
        var max = 0;
        for(var i = 0; i < arr.length; i++) {
            var t = arr[i].toString().length;
            if (max < t) {
                max = t;
            }
        }
        var k = 0, n = 1, m = 1;
        var tmp = [];
        var order = [];
        for(var i = 0; i < 10; i++) {
            tmp[i] = [];
            order[i] = 0;
            for(var j = 0; j < arr.length; j++) {
                tmp[i][j] = 0;
            }
        }
        while(m <= max) {
            for(var i = 0; i < arr.length; i++) {
                var l = Math.floor((arr[i] / n) % 10);
                tmp[l][order[l]] = arr[i];
                order[l]++;
            }
            for(var i = 0; i < 10; i++) {
                if (order[i] != 0) {
                    for(var j = 0; j < order[i]; j++) {
                        arr[k] = tmp[i][j];
                        k++;
                    }
                    order[i] = 0;
                }
            }
            n *= 10;
            k = 0;
            m++;
        }
        return arr;
    }
```