## [The largest difference](https://bigfrontend.dev/problem/Find-the-largest-difference)

<!-- notecardId: 1739477349668 -->

```js
function largestDiff(arr) {
  if (arr.length < 2) return 0;

  let min = Infinity;
  let max = -Infinity;

  for (let i = 0; i < arr.length; i += 1) {
    min = Math.min(min, arr[i]);
    max = Math.max(max, arr[i]);
  }

  return Math.abs(min - max);
}
```
