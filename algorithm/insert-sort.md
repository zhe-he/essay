# 插入排序
![插入排序](../source/images/algorithm/insert.gif)

### 定义
将一个记录插入到已经排好序的有序表中，从而一个新的、记录数增1的有序表。

### 思路
1. 默认一个空的有序数组，第一个元素放入其中
1. 把下一个元素插入到有序数组中
1. 直到没有下一个元素为止

### 代码
1. 第一步:
```
    var arr = [9, 7, 8, 2, 5, 1, 3, 6, 4];
    for(var i = 1; i > 0; i--) {
        if (arr[i] < arr[i - 1]) {
            // 交换位置
            [arr[i], arr[i - 1]] = [arr[i - 1], arr[i]];
        }
    }
```
1. 第二步:
```
    /**
     * 用一个变量记录有序排序的个数
     * 每次和有序数组队尾比较，如果比之大，则排下一个元素，如果比之小，则交换位置，继续和队尾没有比较的元素进行比较
     * 比较完成后，变量+1
     * 直到变量值为数组长度为止
     */
    var arr = [9, 7, 8, 2, 5, 1, 3, 6, 4];
    var n = 1;
    while(n < arr.length) {
        for(var i = n; i > 0; i--) {
            if (arr[i] < arr[i - 1]) {
                // 交换位置
                [arr[i], arr[i - 1]] = [arr[i - 1], arr[i]];
            } else {
                break;
            }
        }
        n++;
    }

```
1. 封装
```
    function insertSort(arr) {
        var n = 1;
        while(n < arr.length) {
            for(var i = n; i > 0; i--) {
                if (arr[i] < arr[i - 1]) {
                    // 交换位置
                    [arr[i], arr[i - 1]] = [arr[i - 1], arr[i]];
                } else {
                    break;
                }
            }
            n++;
        }
        return arr;
    }
    // 调用
    var arr = [9, 7, 8, 2, 5, 1, 3, 6, 4];
    insertSort(arr);
```
1. 优化
```
    function insertSort(arr) {
        for(var i = 1; i < arr.length; i++) {
            for(var j = i; j > 0 && arr[j] < arr[j - 1]; j--) {
                // 交换位置
                [arr[j], arr[j - 1]] = [arr[j - 1], arr[j]];
            }
        }
        return arr;
    }
```
