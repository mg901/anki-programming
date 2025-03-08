## [Indexes of Subarray Sum](https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card)

```js
function subarraySum(arr, target) {
  let left = 0;
  let current = 0;

  for (let right = 0; right < arr.length; right += 1) {
    current += arr[right];

    while (current > target) {
      current -= arr[left];
      left += 1;
    }

    if (current === target) {
      return [left + 1, right + 1];
    }
  }

  return [-1];
}
```
