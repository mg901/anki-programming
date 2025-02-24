## Cyclic Sort

<!-- notecardId: 1739968563075 -->

```js
function cyclicSort(arr) {
  let i = 0;

  while (i < arr.length) {
    const correctIdx = arr[i] - 1;

    if (arr[i] > 0 && arr[i] <= arr.length && arr[i] !== arr[correctIdx]) {
      swap(arr, correctIdx, i);
    } else {
      i += 1;
    }
  }
}

function swap(arr, from, to) {
  const temp = arr[to];
  arr[to] = arr[from];
  arr[from] = temp;
}
```
