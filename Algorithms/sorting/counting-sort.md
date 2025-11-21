## [Counting Sort](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1763667542523 -->

```js
// - Time: O(n + k)
// - Space: O(k)
//   where:
//     k = freq.length
function sortArray(nums) {
  if (nums.length < 2) return nums;

  const min = Math.min(...nums);
  const max = Math.max(...nums);

  const size = max - min + 1;
  const freq = new Array(size).fill(0);

  for (const num of nums) {
    freq[num - min] += 1;
  }

  const result = [];

  for (let i = 0; i < size; i += 1) {
    while (freq[i] > 0) {
      result.push(i + min);
      freq[i] -= 1;
    }
  }

  return result;
}
```
