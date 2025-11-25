## [1046 Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)

```js
function lastStoneWeight(stones) {
  const maxpq = new MaxPriorityQueue();

  stones.forEach((stone) => {
    maxpq.enqueue(stone);
  });

  while (maxpq.size() > 1) {
    const y = maxpq.dequeue();
    const x = maxpq.dequeue();

    if (x !== y) {
      maxpq.enqueue(y - x);
    }
  }

  return maxpq.front() ?? 0;
}
```
