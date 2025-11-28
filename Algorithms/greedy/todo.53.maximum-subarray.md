## [53 Maximum Subarray 'greedy'](https://leetcode.com/problems/maximum-subarray/description/)

```js
function maxSubArray(nums) {
  let max = -Infinity;
  let sum = 0;

  for (const num of nums) {
    sum += num;
    max = Math.max(max, sum);

    if (sum < 0) {
      sum = 0;
    }
  }

  return max;
}
```
