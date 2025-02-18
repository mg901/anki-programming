## [Bubble Sort](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1739879461743 -->

```js
function bubbleSort(arr) {
  const { length } = arr;
  if (length < 2) return arr;

  for (let i = 0; i < length - 1; i += 1) {
    for (let j = 0; j < length - i - 1; j += 1) {
      if (arr[j] > arr[j + 1]) {
        const temp = arr[j + 1];
        arr[j + 1] = arr[j];
        arr[j] = temp;
      }
    }
  }
}
```

## [Bubble Sort 'optimized'](https://bigfrontend.dev/problem/implement-Bubble-Sort)

<!-- notecardId: 1739879461745 -->

```js
function bubbleSort(arr) {
  let { length } = arr;
  if (length < 2) return arr;

  let swapped;

  do {
    swapped = false;

    for (let i = 0; i < length - 1; i += 1) {
      if (arr[i] > arr[i + 1]) {
        const temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;

        swapped = true;
      }
    }

    length -= 1;
  } while (swapped);

  return arr;
}
```
