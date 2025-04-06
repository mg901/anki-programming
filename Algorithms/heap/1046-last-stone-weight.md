## [1046 Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)

<!-- notecardId: 1743966833978 -->

```js
function lastStoneWeight(stones) {
  if (!stones.length) return 0;

  const pq = new MaxPriorityQueue();

  stones.forEach((stone) => {
    pq.enqueue(stone);
  });

  while (pq.size() > 1) {
    const x = pq.dequeue();
    const y = pq.dequeue();

    if (x !== y) {
      pq.enqueue(x - y);
    }
  }

  return pq.front() ?? 0;
}
```
