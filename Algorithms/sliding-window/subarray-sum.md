## [Subarray sum](https://algo.monster/problems/subarray_sum_fixed)

```js
function subarraySumFixed(nums, k) {
  let left = 0;
  let sum = 0;
  let max = 0;

  for (let right = 0; right < nums.length; right += 1) {
    sum += nums[right];

    if (right >= k - 1) {
      max = Math.max(max, sum);

      sum -= nums[left];
      left += 1;
    }
  }

  return max;
}
```
