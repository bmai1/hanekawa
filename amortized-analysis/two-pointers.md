# 👹 two pointers

Concept: Two pointers iterate through array (one at first and last index of SA), each move 1 dir

```
Applicability of 2ptr depends on relation of window scopes:
 1. If a wider scope is invalid, narrower scope must also be invalid
 2. If a wider scope of the sliding window is valid, the narrower scope of that wider scope must remain (potentially) valid
 - vice versa, contrapositive
 
- Subarray Sum: 
  On each turn, the left pointer moves one step to the right, 
  right pointer moves to the right as long as the resulting subarray sum is at most x
  If the sum becomes exactly x, a solution has been found.
```

[3Sum](https://leetcode.com/problems/3sum/): two pointers inside a loop for O(n^2) total time complexity

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        // Sort required for two pointers (triplet order does not matter)
        sort(nums.begin(), nums.end());
        vector<vector<int>> triplets;
        for (int i = 0; i < nums.size(); ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int left = i + 1, right = nums.size() - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                // Sum is too small, so only way to find valid triplet 
                // is to shift left up and increase sum
                if (sum < 0) {
                    ++left;
                }
                // Reverse logic applies
                else if (sum > 0) {
                    --right;
                }
                else {
                    triplets.push_back({nums[i], nums[left], nums[right]});
                    // Logic to skip duplicate triplets
                    int left_prev = nums[left], right_prev = nums[right];
                    while (left < right && nums[left] == left_prev) ++left;
                    while (left < right && nums[right] == right_prev) --right;
                }
            }
        }
        return triplets;
    }
};
```

