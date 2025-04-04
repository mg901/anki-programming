## [1046 Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)

<!-- notecardId: 1743766568179 -->

```js
function lastStoneWeight(stones) {
  const pq = new MaxPriorityQueue();

  stones.forEach((stone) => pq.enqueue(stone));

  while (pq.size() > 1) {
    const a = pq.dequeue();
    const b = pq.dequeue();
    const diff = a - b;

    if (diff > 0) {
      pq.enqueue(diff);
    }
  }

  return pq.front() ?? 0;
}
```
