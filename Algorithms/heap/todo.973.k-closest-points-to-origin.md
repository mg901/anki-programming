## [973 K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/)

```js
function kClosest(points, k) {
  const pq = new MaxPriorityQueue((item) => item[0]);

  for (const [x, y] of points) {
    const distance = x ** 2 + y ** 2;

    pq.enqueue([distance, x, y]);

    if (pq.size() > k) {
      pq.dequeue();
    }
  }

  return pq.toArray().map(([_, x, y]) => [x, y]);
}
```
