## [Merge Sort 'in-place'](https://bigfrontend.dev/problem/implement-Merge-Sort)

```js
// Type: Stable

// - Time: O(n^2)
// - Space: O(h)
function mergeSort(arr, left = 0, right = arr.length - 1) {
  if (left >= right) return;

  const mid = left + ((right - left) >> 1);
  mergeSort(arr, left, mid);
  mergeSort(arr, mid + 1, right);
  merge(arr, left, mid, right);
}

function merge(arr, left, mid, right) {
  let i = left;
  let j = mid + 1;

  while (i <= mid && j <= right) {
    if (arr[i] < arr[j]) {
      i += 1;
    } else {
      const min = arr[j];
      let index = j;

      while (index > i) {
        arr[index] = arr[index - 1];
        index -= 1;
      }

      arr[i] = min;

      i += 1;
      j += 1;
      mid += 1;
    }
  }
}
```

## [Merge Sort 'immutable'](https://www.greatfrontend.com/questions/algo/merge-sort?format=algo)

```js
// Type: Stable

// - Time: O(n log(n))
// - Space: O(n)
function mergeSort(arr) {
  const { length } = arr;
  if (length < 2) return arr;

  const mid = Math.floor(length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(leftArr, rightArr) {
  let leftIndex = 0;
  let rightIndex = 0;
  const result = [];

  while (leftIndex < leftArr.length && rightIndex < rightArr.length) {
    if (leftArr[leftIndex] <= rightArr[rightIndex]) {
      result.push(leftArr[leftIndex]);
      leftIndex += 1;
    } else {
      result.push(rightArr[rightIndex]);
      rightIndex += 1;
    }
  }

  result.push(...leftArr.slice(leftIndex), ...rightArr.slice(rightIndex));

  return result;
}
```
