## [Selection Sort](https://bigfrontend.dev/problem/implement-Selection-Sort)

<!-- notecardId: 1760896167243 -->

```js
// Explanation:
// CS50: https://youtu.be/uCbV2xHxalk

// Type: Unstable

// - Time: O(n^2)
// - Space: O(1)
function selectionSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  let minIndex;

  for (let i = 0; i < n - 1; i += 1) {
    minIndex = i;

    for (let j = i + 1; j < n; j += 1) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    if (minIndex !== i) {
      swap(arr, i, minIndex);
    }
  }
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
