## [Reorder array with new indexes](https://bigfrontend.dev/problem/reorder-array-with-new-indexes)

<!-- notecardId: 1740329979541 -->

```js
// - Time: O(n)
// - Space: O(1)
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

function swap(arr, from, to) {
  const temp = arr[to];
  arr[to] = arr[from];
  arr[from] = temp;
}
```
