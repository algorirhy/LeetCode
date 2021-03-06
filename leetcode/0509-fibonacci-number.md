# [斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

f(0) = 0, f(1) = 1, f(2)=1;

### 方法一

```java
class Solution {
    public int fib(int n) {
        if (n < 2) {
            return n;
        }
        int f1 = 0, f2 = 1;
        for (int i = 2; i <= n; i++) {
            int tmp = f1 + f2;
            f1 = f2;
            f2 = tmp % 1000000007;
        }
        return f2;
    }
}
```

### 方法二

动态规划

```java
class Solution {
    public int fib(int n) {
        if (n < 2) {
            return n;
        }
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
            dp[i] %= 1000000007;
        }
        return dp[n];
    }
}
```
