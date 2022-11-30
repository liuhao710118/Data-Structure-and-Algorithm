## 差分数组参考文章

1. [小而美的算法技巧：差分数组 :: labuladong的算法小抄 (gitee.io)](https://labuladong.gitee.io/algo/2/20/25/)
2. [(2条消息) 前缀和与差分 图文并茂 超详细整理（全网最通俗易懂）_林小鹿@的博客-CSDN博客_前缀和差分](https://blog.csdn.net/weixin_45629285/article/details/111146240)





题目链接：[https://leetcode.cn/problems/range-sum-query-2d-immutable/](https://leetcode.cn/problems/range-sum-query-2d-immutable/)

题目难度：中等

题解源码：

```java
class NumMatrix {

        private int[][] matrix;

        private int[][] dp;

        public NumMatrix(int[][] matrix) {
            int m = matrix.length, n = matrix[0].length;
            if (m == 0 || n == 0) {
                return;
            }
            this.matrix = matrix;
            this.dp = new int[this.matrix.length + 1][this.matrix[0].length + 1];
            for (int i = 1; i < this.dp.length; i++) {
                for (int j = 1; j < this.dp[i].length; j++) {
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1] + matrix[i - 1][j - 1] - dp[i - 1][j - 1];
                }
            }
        }

        public int sumRegion(int x1, int y1, int x2, int y2) {

            return dp[x2 + 1][y2 + 1] - dp[x2 + 1][y1] - dp[x1][y2 + 1] + dp[x1][y1];
            
        }
    }

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```

![image-20221130230239696](resources/leetcode304.%E4%BA%8C%E7%BB%B4%E5%8C%BA%E5%9F%9F%E5%92%8C%E6%A3%80%E7%B4%A2%20-%20%E7%9F%A9%E9%98%B5%E4%B8%8D%E5%8F%AF%E5%8F%98.assets/image-20221130230239696.png)