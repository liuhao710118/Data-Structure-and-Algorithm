## 差分数组参考文章

1. [小而美的算法技巧：差分数组 :: labuladong的算法小抄 (gitee.io)](https://labuladong.gitee.io/algo/2/20/25/)
2. [(2条消息) 前缀和与差分 图文并茂 超详细整理（全网最通俗易懂）_林小鹿@的博客-CSDN博客_前缀和差分](https://blog.csdn.net/weixin_45629285/article/details/111146240)







题目链接：https://leetcode.cn/problems/range-sum-query-immutable/

题目难度：简单

题解源码：

```java
class NumArray {

        private int[] nums;

        private int[] a;

        public NumArray(int[] nums) {
            this.nums = nums;
            a = new int[nums.length];
            a[0] = nums[0];
            for (int i = 1; i < nums.length; i++) {
                a[i] = nums[i] + a[i - 1];
            }
        }

        public int sumRange(int left, int right) {
            if (left == right && left == 0) {
                return a[left];
            }
            if (left == 0) {
                return a[right];
            }
            return a[right] - a[left - 1];
        }

    }

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(left,right);
 */
```

![image-20221130214704367](resources/leetcode303.%E4%B8%80%E7%BB%B4%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E5%89%8D%E7%BC%80%E5%92%8C.assets/image-20221130214704367.png)