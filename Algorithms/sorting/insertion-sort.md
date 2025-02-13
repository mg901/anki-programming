## [Insertion Sort](https://bigfrontend.dev/problem/implement-Insertion-Sort)

<!-- notecardId: 1739192654703 -->

```js
function insertionSort(arr) {
  const { length } = arr;
  if (length < 2) return arr;

  for (let i = 1; i < length; i += 1) {
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
