## [Smallest subarray with sum greater than x](https://www.geeksforgeeks.org/problems/smallest-subarray-with-sum-greater-than-x5651/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card)

```js
function smallestSubWithSum(arr, x) {
  let smallest = Infinity;
  let sum = 0;
  let start = 0;

  for (let end = 0; end < arr.length; end += 1) {
    sum += arr[end];

    while (sum > x) {
      smallest = Math.min(smallest, end - start + 1);

      sum -= arr[start];
      start += 1;
    }
  }

  return smallest === Infinity ? 0 : smallest;
}
```
