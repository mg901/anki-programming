## [703 Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)

```js
class KthLargest {
  constructor(k, nums) {
    this.k = k;
    const minpq = new MinPriorityQueue();

    for (const num of nums) {
      minpq.enqueue(num);

      if (minpq.size() > k) {
        minpq.dequeue();
      }
    }

    this.minpq = minpq;
  }

  add(val) {
    this.minpq.enqueue(val);

    if (this.minpq.size() > this.k) {
      this.minpq.dequeue();
    }

    return this.minpq.front();
  }
}
```
