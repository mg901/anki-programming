## [53 Maximum Subarray 'greedy'](https://leetcode.com/problems/maximum-subarray/description/)

```js
function maxSubArray(nums) {
  let maxSum = -Infinity;
  let sum = 0;

  for (const num of nums) {
    sum += num;
    maxSum = Math.max(maxSum, sum);

    if (sum < 0) {
      sum = 0;
    }
  }

  return maxSum;
}
```
