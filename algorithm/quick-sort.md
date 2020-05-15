# 快速排序
![快速排序](../source/images/algorithm/quick.gif)

### 定义
通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

### 代码
```
    function quickSort(arr) {
        function sort(arr, left, right) {
            if (left < right) {
                var i = left;
                var j = right;
                var key = arr[j];
                while(i < j) {
                    while(i < j && arr[i] <= key) {
                        i++;
                    }
                    arr[j] = arr[i]; // 较大值放在右边
                    while(j > i && arr[j] >= key) {
                        j--;
                    }
                    arr[i] = arr[j]; // 较小值放在左边
                }
                arr[i] = arr[j];
                arr[j] = key;
                sort(arr, left, j - 1);
                sort(arr, j + 1, right);
            }
        }
        sort(arr, 0, arr.length - 1);
        return arr;
    }
```