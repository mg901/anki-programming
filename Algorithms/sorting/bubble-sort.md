## [Bubble Sort](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1760737338357 -->

```js
// Type: Stable

// - Time: O(n^2)
// - Space: O(1)
function bubbleSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  for (let i = 0; i < n - 1; i += 1) {
    for (let j = 0; j < n - i - 1; j += 1) {
      if (arr[j] > arr[j + 1]) {
        swap(arr, j, j + 1);
      }
    }
  }
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```

## [Bubble Sort 'optimized'](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1760737338362 -->

```js
// Type: Stable

// - Time: O(n^2)
// - Space: O(1)
function bubbleSort(arr) {
  let n = arr.length;
  if (n < 2) return;

  let swapped;

  do {
    swapped = false;

    for (let i = 1; i < n; i += 1) {
      if (arr[i - 1] > arr[i]) {
        swap(arr, i - 1, i);
        swapped = true;
      }
    }

    n -= 1;
  } while (swapped);
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
