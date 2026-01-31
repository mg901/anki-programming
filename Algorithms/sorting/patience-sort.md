## [Patience Sort](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1767542252773 -->

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
  const n = nums.length;
  if (n < 2) return nums;

  const piles = buildPiles(nums);

  return mergePiles(piles);
}

// Source: [3,7,5,6,4,2]

// Sorted:
//  3  7  6
//  2  5
//     4
function buildPiles(nums) {
  const piles = [];

  for (const num of nums) {
    let left = 0;
    let right = piles.length;

    while (left < right) {
      const mid = left + ((right - left) >> 1);
      const last = piles[mid].at(-1);

      if (num <= last) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }

    (piles[left] ??= []).push(num);
  }

  return piles;
}

function mergePiles(piles) {
  const minHeap = new MinHeap((item) => item.val);

  for (const pile of piles) {
    minHeap.push({
      val: pile.pop(),
      pile,
    });
  }

  const result = [];

  while (!minHeap.isEmpty()) {
    const smallest = minHeap.pop();
    result.push(smallest.val);

    if (smallest.pile.length) {
      smallest.val = smallest.pile.pop();
      minHeap.push(smallest);
    }
  }

  return result;
}
```
