## [Reorder array with new indexes](https://bigfrontend.dev/problem/reorder-array-with-new-indexes)

<!-- notecardId: 1739659596775 -->

```js
function sort(items, newOrder) {
  let index = 0;

  while (index < items.length) {
    if (newOrder[index] !== index) {
      const newIndex = newOrder[index];

      swap(items, newIndex, index);
      swap(newOrder, newIndex, index);
    } else {
      index += 1;
    }
  }
}

function swap(arr, a, b) {
  const temp = arr[b];
  arr[b] = arr[a];
  arr[a] = temp;
}
```
