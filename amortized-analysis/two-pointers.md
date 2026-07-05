# 👹 two pointers

Three common variations of two pointers:

* Converging: one point at start, one at end (len - 1)
  * Sorted arrays, palindromes, target pairs
* Fast and slow: start same index, different speed
  * Linked list cycle
* Sliding window: same direction, one contract other expand

Hints: modify array in-place O(1) memory, nested loop comparison brute force



**Remove Duplicates from Sorted Array**

Fast and slow:&#x20;

* fast pointer scans array looking for new elements
* slow pointer tracks unique count and position to place new element

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        // Because it is sorted, the first element 
        // will always be in the right position
        int k = 1;
        for (int i = 1; i < nums.size(); ++i) {
            // Note k-1 for zero indexing
            if (nums[i] != nums[k - 1]) {
                nums[k++] = nums[i];
            }
        }
        return k;
    }
};
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

