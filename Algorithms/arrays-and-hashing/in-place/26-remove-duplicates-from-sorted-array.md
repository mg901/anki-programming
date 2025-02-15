## [26 Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

<!-- notecardId: 1739659589571 -->

```js
function removeDuplicates(nums) {
  let i = 0;
  for (let j = 0; j < nums.length; j += 1) {
    if (nums[j] !== nums[i]) {
      nums[(i += 1)] = nums[j];
    }
  }

  nums.splice(i + 1);

  return nums.length;
}
```
