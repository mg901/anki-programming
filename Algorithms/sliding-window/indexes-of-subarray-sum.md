## [Indexes of Subarray Sum](https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card)

```js
function subarraySum(arr, target) {
  let sum = 0;
  let start = 0;

  for (let end = 0; end < arr.length; end += 1) {
    sum += arr[end];

    while (sum > target) {
      sum -= arr[start];
      start += 1;
    }

    if (sum === target) {
      return [start + 1, end + 1];
    }
  }

  return [-1];
}
```
