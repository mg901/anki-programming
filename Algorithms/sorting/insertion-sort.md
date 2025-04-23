## [Insertion Sort](https://bigfrontend.dev/problem/implement-Insertion-Sort)

<!-- notecardId: 1745329176860 -->

```js
function insertionSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  for (let i = 1; i < n; i += 1) {
    const current = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j -= 1;
    }

    arr[j + 1] = current;
  }
}
```
