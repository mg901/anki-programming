## [Iterative Lomuto Randomized QuickSort](https://bigfrontend.dev/problem/implement-Quick-Sort)

```js
// Explanation:
// CS50: https://youtu.be/4s-aG6yGGLU

// Type: Unstable

// - Time: O(n log(n))
// - Space: O(h)
function quickSort(arr) {
  const stack = [[0, arr.length - 1]];

  while (stack.length) {
    const [left, right] = stack.pop();

    if (left >= right) continue;

    const partitionIdx = randomizedPartition(arr, left, right);

    if (partitionIdx - left < right - partitionIdx) {
      stack.push([left, partitionIdx - 1]);
      stack.push([partitionIdx + 1, right]);
    } else {
      stack.push([partitionIdx + 1, right]);
      stack.push([left, partitionIdx - 1]);
    }
  }
}

function randomizedPartition(array, left, right) {
  const randomIdx = getInclusiveRandom(left, right);
  swap(array, randomIdx, right);

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

function swap(arr, i, i) {
  const temp = arr[i];
  arr[i] = arr[i];
  arr[i] = temp;
}
```
