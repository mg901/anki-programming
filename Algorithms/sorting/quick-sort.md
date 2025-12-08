## [Quick Sort 'Naive Lomuto Partition'](https://www.greatfrontend.com/questions/algo/quick-sort)

<!-- notecardId: 1765041774298 -->

```js
// Explanation:
// CS50: https://youtu.be/4s-aG6yGGLU

// Type: Unstable

// - Time:
//    Average: O(n log(n))
//    Worst: O(n^2)

// Space:
//    Average: O(n log n)
//    Worst: O(n^2)
export default function quickSort(arr) {
  const n = arr.length;
  if (n < 2) return arr;

  const pivot = arr[n - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < n - 1; i += 1) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return quickSort(left).concat(pivot, ...quickSort(right));
}
```

## [Quick Sort 'Randomized Lomuto Partition'](https://bigfrontend.dev/problem/implement-Quick-Sort)

<!-- notecardId: 1765041774299 -->

```js
// Explanation:
// CS50: https://youtu.be/4s-aG6yGGLU

// Type: Unstable

// Technique: Stack Optimization (Tail Recursion Elimination)

// - Time:
//    Average: O(n log(n))
//    Worst: O(n^2)

// Space:
//    Average: O(log n)
//    Worst: O(n)
function quickSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  const stack = [[0, n - 1]];

  while (stack.length) {
    let [left, right] = stack.pop();

    while (left < right) {
      // low <= pivotIdx - 1
      // pivotIdx + 1 >= high
      const pivotIdx = randomizedPartition(arr, left, right);

      if (pivotIdx - left < right - pivotIdx) {
        stack.push([pivotIdx + 1, right]);
        right = pivotIdx - 1;
      } else {
        stack.push([left, pivotIdx - 1]);
        left = pivotIdx + 1;
      }
    }
  }
}

function randomizedPartition(arr, left, right) {
  const randomIdx = randomInclusive(left, right);
  swap(arr, right, randomIdx);

  return lomutoPartition(arr, left, right);
}

function randomInclusive(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function lomutoPartition(arr, left, right) {
  const pivot = arr[right];
  let wall = left;

  for (let i = left; i < right; i += 1) {
    if (arr[i] <= pivot) {
      if (wall !== i) {
        swap(arr, i, wall);
      }

      wall += 1;
    }
  }

  if (wall !== right) {
    swap(arr, wall, right);
  }

  return wall;
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```

## [Quick Sort 'Randomized Haore Partition'](https://bigfrontend.dev/problem/implement-Quick-Sort)

<!-- notecardId: 1765041774300 -->

```js
// Explanation:
// Bukan Cara Cepat: https://youtu.be/NuQYFXmLUrM

// Type: Unstable

// - Time:
//    Average: O(n log(n))
//    Worst: O(n^2)

// Space:
//    Average: O(log n)
//    Worst: O(n)
function quickSort(arr) {
  const n = arr.length;
  if (n < 2) return;

  const stack = [[0, n - 1]];

  while (stack.length) {
    let [left, right] = stack.pop();

    while (left < right) {
      // low <= boundary
      // boundary + 1 <= high
      const boundary = randomizedPartition(arr, left, right);

      if (boundary - left < right - boundary) {
        stack.push([boundary + 1, right]);
        right = boundary;
      } else {
        stack.push([left, boundary]);
        left = boundary + 1;
      }
    }
  }
}

function randomizedPartition(arr, left, right) {
  const randomIdx = randomInclusive(left, right);
  swap(arr, randomIdx, left);

  return hoarePartition(arr, left, right);
}

function randomInclusive(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function hoarePartition(arr, left, right) {
  const pivot = arr[left];
  let i = left - 1;
  let j = right + 1;

  while (true) {
    do i += 1;
    while (arr[i] < pivot);

    do j -= 1;
    while (arr[j] > pivot);

    if (i >= j) return j;

    swap(arr, i, j);
  }
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
