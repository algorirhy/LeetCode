# [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

### 方法一

双端队列

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int len = nums.length;
        if (k * len == 0) return new int[0];
        if (k == 1) return nums;
        int[] res = new int[len - k + 1];
        Deque<Integer> deq = new ArrayDeque<>();
        for (int i = 0; i < len; i++) {
            //保证队列首元素为当前窗口最大值下标
            while(!deq.isEmpty() && nums[deq.getLast()] <= nums[i]) {
                deq.removeLast();
            }
            //队首元素坐标对应的num不在窗口中，需要弹出
            if (!deq.isEmpty() && i - deq.getFirst() + 1 > k) {
                deq.removeFirst();
            }
            deq.addLast(i);
            if (i + 1 >= k) {
                res[i - k + 1] = nums[deq.getFirst()];
            }
        }
        return res;
    }
}
```

### 方法二

动态规划

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int len = nums.length;
        if (k * len == 0) 
            return new int[0];
        if (k == 1) return nums;
        int[] res = new int[len - k + 1];

        int[] left = new int[len];
        left[0] = nums[0];
        int[] right = new int[len];
        right[len - 1] = nums[len - 1];

        for (int i = 1; i < len; i++) {
            if (i % k == 0) left[i] = nums[i];
            else left[i] = Math.max(left[i - 1], nums[i]);

            int j = len - i - 1;
            if ((j + 1) % k == 0) right[j] = nums[j];
            else right[j] = Math.max(right[j + 1], nums[j]);
        }

        for (int i = 0; i < len - k + 1; i++) {
            res[i] = Math.max(left[i + k - 1], right[i]);
        }
        return res;
    }
}
```

