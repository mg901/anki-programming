## [215 Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

```js
function findKthLargest(nums, k) {
  const pq = new MinPriorityQueue();

  for (const num of nums) {
    pq.enqueue(num);

    if (pq.size() > k) {
      pq.dequeue();
    }
  }

  return pq.front();
}
```
