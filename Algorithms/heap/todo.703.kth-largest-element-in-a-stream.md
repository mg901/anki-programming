## [703 Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)

```js
class KthLargest {
  constructor(k, nums) {
    this.k = k;
    const pq = new MinPriorityQueue();

    for (const num of nums) {
      pq.enqueue(num);

      if (pq.size() > k) {
        pq.dequeue();
      }
    }

    this.pq = pq;
  }

  add(val) {
    this.pq.enqueue(val);

    if (this.pq.size() > this.k) {
      this.pq.dequeue();
    }

    return this.pq.front();
  }
}
```
