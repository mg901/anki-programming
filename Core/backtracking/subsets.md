## [Subsets](https://leetcode.com/problems/subsets/description/)

<!-- notecardId: 1763130591766 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/REOH22Xwdkk

// Complexity:
// - Time: O(n * n^2)
// - Space: O(n * n^2)
function subsets(nums) {
  const n = nums.length;
  const result = [];
  backtrack(0, []);

  return result;

  function backtrack(start, subset) {
    result.push([...subset]);

    for (let i = start; i < n; i += 1) {
      subset.push(nums[i]);
      backtrack(i + 1, subset);

      subset.pop();
    }
  }
}
```
