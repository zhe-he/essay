# 碰撞检测
碰撞分为很多种，椭圆与矩形的碰撞，椭圆与椭圆的碰撞，矩形与多边形的碰撞等，本篇仅介绍矩形之间的碰撞，圆形之间的碰撞，矩形与圆形之间的碰撞。    

### 矩形之间的碰撞
矩形a与矩形b之间的碰撞，可以用相反的思路来实现，如果a在b的左边、上面、右边、下面则a和b没有碰撞。    
getBoundingClientRect返回的top、right、bottom、left如图：
![getBoundingClientRect](../../source/images/function/bounding_client_rect.png)
```
    function collisionCheckRect(div1, div2) {
        var rect1 = div1.getBoundingClientRect();
        var rect2 = div2.getBoundingClientRect();

        if (rect1.right < rect2.left) {
            // div1在div2的左边
            return false;
        }
        if (rect1.bottom > rect2.top) {
            // div1在div2的上面
            return false;
        }
        if (rect1.left > rect2.right) {
            // div1在div2的右边
            return false;
        }
        if (rect1.top < rect2.bottom) {
            // div1在div2的下面
            return false;
        }
        // 如果都不是，则为碰撞
        return true;
    }
```

### 优化矩形之间的碰撞
```
// 做一个简单的计算：
a || b || c || d = !!(a || b || c || d)
                 = !(!a && !b && !c && !d)
// 上面的代码可以写成
if(rect1.right < rect2.left || rect1.bottom > rect2.top || rect1.left > rect2.right || rect1.top < rect2.bottom) {
    return false;
} else {
    return true;
}
// 也可以写成
function collisionCheckRect(div1, div2) {
    var rect1 = div1.getBoundingClientRect();
    var rect2 = div2.getBoundingClientRect();

    if (rect1.right >= rect2.left && rect1.bottom <= rect2.top && rect1.left <= rect2.right && rect1.top >= rect2.bottom) {
        return true;
    } else {
        return false;
    }
}
```

### 圆形之间的碰撞
圆形之间的碰撞较为简单，计算两个圆心的距离是否小于等于两圆半径之和即可：    
```
    class Circle{
        x = 0;
        y = 0;
        r = 0;
        constructor(x, y, r) {
           this.x = x;
           this.y = y;
           this.r = r;
        }
    }

    function collisionCheckCircle(circle1, circle2) {
        return Math.sqrt(Math.pow(circle1.x - circle2.x, 2) + Math.pow(circle1.y - circle2.y, 2)) <= circle1.r + circle2.r;
    }

    var a = new Circle(2, 2, 2);
    var b = new Circle(1, 1, 1);
    collisionCheckCircle(a, b);
```
程序计算平方比平方根快很多，函数可以改成如下
```
    function collisionCheckCircle(circle1, circle2) {
        return (circle1.x - circle2.x) ** 2 + (circle1.y - circle2.y) ** 2 <= (circle1.r + circle2.r) ** 2;
    }
```

### 矩形与圆形之间的碰撞
1. 把矩形上下左右分别扩充R(圆的半径)的长度形成一个新的矩形，如果圆心在新的矩形内，则发生碰撞
2. 如果上述条件不成立，圆只可能在矩形4个顶点周围碰撞，计算4个顶点的到圆心的距离，如果小于半径R则碰撞

```
    class Rect{
        x = 0; // 左上角坐标x
        y = 0; // 左上角坐标y
        w = 0;
        h = 0;
    }

    function collisionCheckPoint(x1, y1, x2, y2, r) {
        return (x1 - x2) ** 2 + (y1 - y2) ** 2 <= r ** 2;
    }

    function collisionCheck(rect, circle) {
        var { x, y ,r } = circle;
        if (x >= rect.x - r && x <= rect.x + rect.w + r && y >= rect.y - r && y <= rect.y + r) {
            return true;
        } else {
            if (
                collisionCheckPoint(rect.x, rect.y, x, y, r) ||
                collisionCheckPoint(rect.x + rect.w, rect.y, x, y, r) ||
                collisionCheckPoint(rect.x, rect.y + rect.h, x, y, r) ||
                collisionCheckPoint(rect.x + rect.w, rect.y + rect.h, x, y, r)
            ) {
                return true;
            } else {
                return false;
            }
        }
    }
```
### 简写
把所有的false分支合并
```
    function collisionCheck(rect, circle) {
        var { x, y ,r } = circle;
        if (
            (x < rect.x - r || x > rect.x + rect.w + r || y < rect.y - r || y > rect.y + r) && 
                !collisionCheckPoint(rect.x, rect.y, x, y, r) &&
                !collisionCheckPoint(rect.x + rect.w, rect.y, x, y, r) &&
                !collisionCheckPoint(rect.x, rect.y + rect.h, x, y, r) &&
                !collisionCheckPoint(rect.x + rect.w, rect.y + rect.h, x, y, r)
        ) {
            return false;
        } else {
            return true;
        }
    }
```
