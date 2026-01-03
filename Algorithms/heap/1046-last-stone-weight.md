## [1046 Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)

<!-- notecardId: 1767104727367 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/B-QCq79-Vfw

// - Time: O(n log(n))
// - Space: O(n)
function lastStoneWeight(stones) {
  const maxHeap = new MaxHeap();

  stones.forEach((stone) => {
    maxHeap.push(stone);
  });

  while (maxHeap.size() > 1) {
    const y = maxHeap.pop();
    const x = maxHeap.pop();

    if (x !== y) {
      maxHeap.push(y - x);
    }
  }

  return maxHeap.top() ?? 0;
}
```
