## [Intersection of two sorted arrays](https://bigfrontend.dev/problem/intersection-of-two0-sorted-Arrays)

<!-- notecardId: 1765471158390 -->

```js
// - Time: O(n + m)
// - Space: O(1)
function intersect(arr1, arr2) {
  const m = arr1.length;
  const n = arr2.length;

  let i = 0;
  let j = 0;
  const result = [];

  while (i < m && j < n) {
    if (arr1[i] === arr2[j]) {
      result.push(arr1[i]);

      i += 1;
      j += 1;
    } else if (arr1[i] < arr2[j]) {
      i += 1;
    } else {
      j += 1;
    }
  }

  return result;
}
```
