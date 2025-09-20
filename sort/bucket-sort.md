---
icon: dog
---

# bucket sort

O(n+k), where k is number of buckets, best for uniform distribution

* Split elements into buckets
* Insertion or other sort buckets
* Recombine buckets

Assume input \[0, 1), otherwise need to normalize to fit into buckets

```java
private static void insertionSort(List<Double> bucket) {
    for (int i = 1; i < bucket.size(); i++) {
        double key = bucket.get(i);
        int j = i - 1;
        while (j >= 0 && bucket.get(j) > key) {
            bucket.set(j + 1, bucket.get(j));
            j--;
        }
        bucket.set(j + 1, key);
    }
}

public static void bucketSort(double a[]) {
    int n = a.length;

    // Create buckets
    List<Double> buckets[] = new ArrayList[n];
    for (int i = 0; i < n; ++i) {
        buckets[i] = new ArrayList<>();
    }

    // If input [0, 1), don't need to normalize doubles
    for (double val : a) {
        int i = (int) (val * n);
        buckets[i].add(val);
    }

    // Sort buckets
    for (List<Double> bucket : buckets) {
        insertionSort(bucket);
    }

    // Concatenate
    int index = 0;
    for (List<Double> bucket : buckets) {
        for (double val : bucket) {
            a[index++] = val;
        }
    }
}
```

