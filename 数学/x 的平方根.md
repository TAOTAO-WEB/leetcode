## [x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**示例 1**:

```
输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

> 测试用例不太友善，一般用二分可以快速做出来，暴力求解会超出时间限制，另外就是可以用数学方法做

```java
public int mySqrt(int x) {
        if(x<=1) return x;
        long start = 1;
        long end = x/2+1;
        while (start<end){
            Long mid = (start+end+1)/2;
            if(mid*mid>x){
                end = --mid;
            }
            else {
                start = mid;
            }
        }
        return (int)start;
    }
```

> 牛顿迭代法，参考评论区大佬

```python
class Solution:
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x <= 1:
            return x
        r = x
        while r > x / r:
            r = (r + x / r) // 2
        return int(r)
```

