## [Subarray sum](https://algo.monster/problems/subarray_sum_fixed)

```js
function subarraySumFixed(nums, k) {
  let left = 0;
  let max = 0;
  let current = 0;

  for (let i = 0; i < k; i += 1) {
    current += nums[i];
  }

  max = current;

  for (let right = k; right < nums.length; right += 1) {
    current += nums[right] - nums[left];
    left += 1;

    max = Math.max(max, current);
  }

  return max;
}
```
