## [973 K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/)

```js
function kClosest(points, k) {
  const maxpq = new MaxPriorityQueue((item) => item[0]);

  for (const [x, y] of points) {
    const distance = x ** 2 + y ** 2;

    maxpq.enqueue([distance, x, y]);

    if (maxpq.size() > k) {
      maxpq.dequeue();
    }
  }

  return maxpq.toArray().map(([_, x, y]) => [x, y]);
}
```
