## [Iterative Lomuto Randomized QuickSort](https://bigfrontend.dev/problem/implement-Quick-Sort)

```js
// // Type: Unstable

// - Time: O(n log(n))
// - Space: O(h)
function quickSort(arr) {
  const stack = [[0, arr.length - 1]];

  while (stack.length) {
    const [left, right] = stack.pop();

    if (left >= right) continue;

    const partitionIndex = randomizedPartition(arr, left, right);

    if (partitionIndex - left < right - partitionIndex) {
      stack.push([left, partitionIndex - 1]);
      stack.push([partitionIndex + 1, right]);
    } else {
      stack.push([partitionIndex + 1, right]);
      stack.push([left, partitionIndex - 1]);
    }
  }
}

function randomizedPartition(array, left, right) {
  const randomIndex = getInclusiveRandom(left, right);
  swap(array, randomIndex, right);

  return partition(array, left, right);
}

function getInclusiveRandom(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function partition(array, left, right) {
  const pivot = array[right];
  const i = left;

  for (let j = left; j < right; j += 1) {
    if (array[j] <= pivot) {
      swap(array, j, i);
      i += 1;
    }
  }

  swap(array, i, right);

  return i;
}

function swap(arr, from, to) {
  const temp = arr[to];
  arr[to] = arr[from];
  arr[from] = temp;
}
```
