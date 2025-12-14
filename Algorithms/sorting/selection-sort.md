## [Selection Sort](https://bigfrontend.dev/problem/implement-Selection-Sort)

<!-- notecardId: 1765708006882 -->

```js
// Explanation:
// CS50: https://youtu.be/uCbV2xHxalk

// Type: Unstable

// - Time: O(n^2)
// - Space: O(1)
function selectionSort(arr) {
  const n = arr.length;
  if (n < 2) return arr;

  let minIndex;

  for (let i = 0; i < n - 1; i += 1) {
    minIndex = i;

    for (let j = i + 1; j < n; j += 1) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }
}
```
