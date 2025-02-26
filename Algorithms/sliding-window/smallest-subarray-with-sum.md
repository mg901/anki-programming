## [Smallest subarray with sum greater than a given value](https://www.geeksforgeeks.org/minimum-length-subarray-sum-greater-given-value/#expected-approach-using-two-pointers-on-time-and-o1-space)

<!-- notecardId: 1740580682386 -->

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

  return smallest;
}
```
