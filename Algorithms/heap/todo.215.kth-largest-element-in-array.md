## [215 Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

```js
function findKthLargest(nums, k) {
  const minpq = new MinPriorityQueue();

  for (const num of nums) {
    minpq.enqueue(num);

    if (minpq.size() > k) {
      minpq.dequeue();
    }
  }

  return minpq.front();
}
```
