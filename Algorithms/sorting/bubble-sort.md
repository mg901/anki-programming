## [Bubble Sort](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1765135957192 -->

```js
// Type: Stable

// - Time:
//    Best: O(n)
//    Average: O(n^2)

// - Space: O(1)
function quickSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  for (let i = 0; i < n - 1; i += 1) {
    for (let j = 1; j < n - i; j += 1) {
      if (arr[j - 1] > arr[j]) {
        [arr[j], arr[j - 1]] = [arr[j - 1], arr[j]];
      }
    }
  }
}
```

## [Bubble Sort 'optimized'](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1765041481032 -->

```js
// Type: Stable

// - Time:
//    Best: O(n)
//    Average: O(n^2)

// - Space: O(1)
function bubbleSort(arr) {
  let n = arr.length;
  if (n < 2) return;

  let swapped;

  do {
    swapped = false;

    for (let i = 1; i < n; i += 1) {
      if (arr[i - 1] > arr[i]) {
        [arr[i], arr[i - 1]] = [arr[i - 1], arr[i]];
        swapped = true;
      }
    }

    n -= 1;
  } while (swapped);
}
```
