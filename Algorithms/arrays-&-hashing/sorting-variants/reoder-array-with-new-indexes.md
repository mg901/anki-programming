## [Reorder array with new indexes](https://bigfrontend.dev/problem/reorder-array-with-new-indexes)

<!-- notecardId: 1767984303652 -->

```js
// - Technique: Cyclic Sort

// - Time: O(n)
// - Space: O(1)
function sort(items, newOrder) {
  const n = items.length;
  let index = 0;

  while (index < n) {
    if (newOrder[index] !== index) {
      const newIndex = newOrder[index];

      swap(items, newIndex, index);
      swap(newOrder, newIndex, index);
    } else {
      index += 1;
    }
  }
}

function swap(arr, i, j) {
  if (i === j) return;

  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
