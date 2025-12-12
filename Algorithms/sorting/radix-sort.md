## [Radix Sort](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1765274356283 -->

```js
// Explanation:
// CS Dojo: https://youtu.be/XiuSW_mEn7g

// - Time: O(n * k)
// - Space: O(n + b)
//   where:
//    n - number of elements
//    k - number of digits per number
//    b - base (usually 10)
function sortArray(nums) {
  const pos = nums.filter((num) => num >= 0);
  const neg = nums.filter((num) => num < 0).map((num) => -num);

  const posSorted = radixSort(pos);
  const negSorted = radixSort(neg)
    .map((num) => -num)
    .reverse();

  return [...negSorted, ...posSorted];
}

function radixSort(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  let place = 1;
  const max = Math.max(...nums);

  while (Math.trunc(max / place) > 0) {
    nums = countingSortForDigits(nums, place);
    place *= 10;
  }

  return nums;
}

function countingSortForDigits(nums, place) {
  const n = nums.length;
  if (n < 2) return nums;

  const RADIX = 10;
  const sorted = new Array(n);
  const counter = new Array(RADIX).fill(0);

  for (const num of nums) {
    const digit = Math.trunc(num / place) % RADIX;
    counter[digit] += 1;
  }

  for (let i = 1; i < RADIX; i += 1) {
    counter[i] += counter[i - 1];
  }

  for (let i = n - 1; i >= 0; i -= 1) {
    const num = nums[i];
    const digit = Math.trunc(num / place) % RADIX;
    counter[digit] -= 1;
    sorted[counter[digit]] = num;
  }

  return sorted;
}
```
