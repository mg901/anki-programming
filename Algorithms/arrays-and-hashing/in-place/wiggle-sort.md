## Wiggle Sort

```js
function wiggleSort(arr) {
  arr.sort((a, b) => a - b);
  for (let i = 1; i < arr.length - 1; i += 2) {
    swap(arr, i, i + 1);
  }

  return arr;
}

function swap(arr, from, to) {
  const temp = arr[to];
  arr[to] = arr[from];
  arr[from] = temp;
}
```
