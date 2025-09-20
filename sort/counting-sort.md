---
icon: cloud-check
---

# counting sort

O(n+k), where k is max element in a, best when k not much more than n.

Assume positive (otherwise subtract min)

* Count occurrences
* Prefix sum
* Add elements to new array starting from back of original array

```java
// k is the max element in a
public static int[] countingSort(int a[], int k) {
    int b[] = new int[a.length];
    int c[] = new int[k + 1];
    for (int i = 0; i < a.length; ++i) {
        ++c[a[i]];
    }
    for (int i = 1; i <= k; ++i) {
        c[i] += c[i - 1];
    }
    // c[i] tells you last index that element i is placed in b
    
    for (int i = a.length - 1; i >= 0; --i) {
        b[c[a[i]] - 1] = a[i];
        --c[a[i]];
    }

    return b;
}
```
