## [Bucket Sort](https://leetcode.com/problems/sort-an-array/description)

<!-- notecardId: 1765714333996 -->

```js
// Explanation:
// Quoc Dat Phung: https://youtu.be/xeT31rm3bN0

// - Time:
//    Best: O(n + k)
//    Average: O(n + k + (n^2 / k))
//    Worst: O(n^2)

// Space: O(n + k)
//  where:
//    k - number of buckets
function bucketSort(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  let min = nums[0];
  let max = nums[0];

  for (const num of nums) {
    min = Math.min(min, num);
    max = Math.max(max, num);
  }

  if (min === max) return nums;

  const range = max - min;
  const buckets = Array.from({ length: n }, () => []);

  for (const num of nums) {
    const normalized = (num - min) / range; // to [0, 1)
    const idx = Math.min(Math.floor(normalized * n), n - 1);
    buckets[idx].push(num);
  }

  return buckets.flatMap(insertionSort);
}

function insertionSort(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  for (let i = 1; i < n; i += 1) {
    const current = nums[i];
    let j = i - 1;

    while (j >= 0 && nums[j] > current) {
      nums[j + 1] = nums[j];
      j -= 1;
    }

    nums[j + 1] = current;
  }

  return nums;
}
```
