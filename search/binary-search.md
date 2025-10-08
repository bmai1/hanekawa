---
description: 'Time complexity: O(logn)'
---

# 🥴 binary search

Binary search <mark style="color:yellow;">generally requires a sorted list of elements</mark>, but can also be applied to more complex problems.

### Intuition:

Initialize low and high (a.k.a left/right, start/end) pointers. Determine the middle index and adjust the start and end pointers with a conditional such that the number of remaining potential answers is halved, and the answer is guaranteed to be found in the new window.

### Generalized template:

```python
def binary_search(array) -> int:
    def condition(value) -> bool:
        pass

    lo = 0, hi = len(array)
    while lo < hi: # lo <= hi ?
        mid = lo + (hi - lo) / 2
        if condition(mid):
            lo = mid 
        else:
            hi = mid + 1
    return lo # mid, hi ? 
```

Important:

* left and right pointers initially cover all possibilities
* adjust boundaries (lo <= hi, mid = hi + lo / 2,)
* design inner conditional to adjust left and right index accordingly (mid, mid + 1, mid - 1, ?)
* decide return condition (lo, mid, hi, ?) to match problem

### Java (CS 46B) Binary Search

```java
public static int recursiveBinarySearch(int nums[], int target, int lo, int hi) {
    if (lo < hi) return -1; 
    // or check if (hi >= lo) {...} else return -1 at bottom
    
    int mid = (lo + hi) / 2;
    if (nums[mid] < target) return recursiveBinarySearch(nums, target, lo, mid - 1);
    else if (nums[mid] > target) return recursiveBinarySearch(nums, target, mid + 1, hi);
    else return mid;
}

public static int binarySearch(int nums[], int target, int lo, int hi) {
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

### C++ STL

* lower\_bound returns a pointer to the first array element whose value is at least x
* upper\_bound returns a pointer to the first array element whose value is larger than x
* equal\_range returns both above pointers

Example of finding if value x exists in array:

```cpp
auto k = lower_bound(array, array + n, x) - array;
if (k < n && array[k] == x) {
    // x found at index k
}
```

More general usage to find an element:

```cpp
std::vector<int> arr = {1, 5, 7, 10};
auto lower_it = std::lower_bound(arr.begin(), arr.end(), 7); // binary search returning iterator for first element not less than 7
auto upper_it = std::upper_bound(arr.begin(), arr.end(), 7); // binary search returning iterator for first element greater than 7

std::cout << *lower_it << std::endl; // 7
std::cout << *upper_it << std::endl; // 10

// if it = arr.end(), DNE
```
