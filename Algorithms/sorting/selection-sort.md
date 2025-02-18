## [Selection Sort](https://bigfrontend.dev/problem/implement-Selection-Sort)

<!-- notecardId: 1739879437593 -->

```js
function selectionSort(arr) {
  const { length } = arr;
  if (length < 2) return arr;

  for (let i = 0; i < length - 1; i += 1) {
    let minIndex = i;

    for (let j = i + 1; j < length; j += 1) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    if (minIndex !== i) {
      const temp = arr[i];
      arr[i] = arr[minIndex];
      arr[minIndex] = temp;
    }
  }

  return arr;
}
```
