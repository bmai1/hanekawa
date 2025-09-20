---
icon: face-pensive
---

# insertion sort

Worst case time complexity: O(n²)

Best case (sorted): O(n)

Two parts, elements from unsorted part is inserted into sorted part with comparison/swap loop.

```java
void insertionSort(int numbers[]) {
   int i, j, tmp;

   for (i = 1; i < numbers.length; ++i) {
      j = i;
      // Insert numbers[i] into sorted part 
      // stop when numbers[i] in correct position
      while (j > 0 && numbers[j] < numbers[j - 1]) {
         swap(numbers[j], numbers[j - 1];
         --j;
      }
   }
}
```

```java
void insertionSort(int numbers[]) {
    for (int i = 1; i < numbers.length; ++i) {
        for (int j = i - 1; j >= 0 && numbers[j] > numbers[j + 1]; --j) {
            swap(numbers[j], numbers[j - 1];
        }
    }
}
```
