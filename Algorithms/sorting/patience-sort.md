## [Patience Sort](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1765542191361 -->

```js
// Explanation:
// - Tutorial Horizon: https://youtu.be/WNJnsmOoTJs?si=mtIaJPHPfuu6D-z3&t=27

// - Time:
//    Best: O(n log(k))
//    Average: O(n log(n))
//      where:
//        k - number of piles

// - Space: O(n)
function sortArray(nums) {
  const piles = buildPiles(nums);

  return mergePiles(piles);
}

function buildPiles(nums) {
  const piles = [];

  for (const num of nums) {
    let left = 0;
    let right = piles.length;

    while (left < right) {
      const mid = left + ((right - left) >> 1);
      const top = piles[mid].at(-1);

      if (num <= top) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }

    (piles[right] ??= []).push(num);
  }

  return piles;
}

function mergePiles(piles) {
  const minpq = new MinPriorityQueue((item) => item.val);
  const sorted = [];

  for (const pile of piles) {
    minpq.enqueue({
      val: pile.pop(),
      pile,
    });
  }

  while (!minpq.isEmpty()) {
    const smallest = minpq.dequeue();
    sorted.push(smallest.val);

    if (smallest.pile.length) {
      smallest.val = smallest.pile.pop();
      minpq.enqueue(smallest);
    }
  }

  return sorted;
}
```
