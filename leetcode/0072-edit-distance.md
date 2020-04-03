# [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

动态规划

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 1; j <= n; j++) {
            dp[0][j] = j;
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    // 增删改
                    dp[i][j] = Math.min(Math.min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) + 1;
                }
            }
        }
        return dp[m][n];
    }
}
```

空间优化

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        int[] dp = new int[n + 1];
        // 初始化第一行
        for (int i = 0; i <= n; i++) {
            dp[i] = i;
        }
        for (int i = 1; i <= m; i++) {
            int tmp = dp[0];
            // 初始化第一列
            dp[0] = i;
            for (int j = 1; j <= n; j++) {
                // pre 相当于 dp[i-1][j-1]
                int pre = tmp;
                // 保存当前
                tmp = dp[j];
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[j] = pre;
                } else {
                    // 增删改
                    dp[j] = Math.min(Math.min(dp[j-1], dp[j]), pre) + 1;
                }
            }
        }
        return dp[n];
    }
}
```
