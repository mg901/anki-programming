## [Intersection of two sorted arrays](https://bigfrontend.dev/problem/intersection-of-two0-sorted-Arrays)

<!-- notecardId: 1739477104916 -->

```js
function intersect(arr1, arr2) {
  let i = 0;
  let j = 0;
  const result = [];

  while (i < arr1.length && j < arr2.length) {
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
