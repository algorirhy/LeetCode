# [2.TwoSum](https://leetcode.com/problems/two-sum/)

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
    map<int, int> mp;
    vector<int> ans;
    int len = (int) nums.size();

    for (int i = 0; i < len; i++) {
        if (mp.find(target - nums[i]) != mp.end()) {
            ans.push_back(mp[target - nums[i]]);
            ans.push_back(i);
            return ans;
        }
        mp[nums[i]] = i;
    }
            return ans;
    }
};
```