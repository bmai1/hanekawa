---
icon: face-tongue-sweat
---

# heapsort

{% content-ref url="/broken/pages/enR8gSBZPITEYcRxW4v7" %}
[Broken link](/broken/pages/enR8gSBZPITEYcRxW4v7)
{% endcontent-ref %}

<pre class="language-java"><code class="lang-java"><strong>public class heap {
</strong>    public static int heap_size;
    public static void max_heapify(int a[], int i) {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int max_i = i;

        if (left &#x3C; heap_size &#x26;&#x26; a[left] > a[i]) {
            max_i = left;
        }
        if (right &#x3C; heap_size &#x26;&#x26; a[right] > a[max_i]) {
            max_i = right;
        }
        // need to recursively fix if not in max heap order
        if (max_i != i) {
            int tmp = a[i];
            a[i] = a[max_i];
            a[max_i] = tmp;
            max_heapify(a, max_i);
        }
    }

    public static void build_max_heap(int a[]) {
        // start from last parent
        for (int i = (a.length - 2) / 2; i >= 0; --i) {
            max_heapify(a, i);
        }
    }

    public static void heap_sort(int a[]) {
        int n = a.length; 
        heap_size = n;
        build_max_heap(a);
        for (int i = n - 1; i > 0; --i) {
            int tmp = a[0];
            a[0] = a[i];
            a[i] = tmp;
            heap_size--;
            max_heapify(a, 0);
        }
    }
}    
</code></pre>
