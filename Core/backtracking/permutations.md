## [Permutations](https://leetcode.com/problems/permutations/description/)

<!-- notecardId: 1763130181595 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/FZe0UqISmUw

// Complexity:
// - Time: O(n * n!)
// - Space: O(n * n!)
function permute(nums) {
  const n = nums.length;
  const result = [];
  backtrack(0);

  return result;

  function backtrack(start) {
    if (start === n) {
      result.push([...nums]);

      return;
    }

    for (let i = start; i < n; i += 1) {
      swap(nums, start, i);
      backtrack(start + 1);
      swap(nums, start, i);
    }
  }
}

function swap(arr, i, j) {
  if (i === j) return;

  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
