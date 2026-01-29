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

  return quickSort(left).concat(pivot, quickSort(right));
}
```

## [Quick Sort 'Randomized Lomuto Partition'](https://bigfrontend.dev/problem/implement-Quick-Sort)

<!-- notecardId: 1766694058340 -->

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
      // low <= pivot - 1
      // pivot + 1 >= high
      const pivot = lomutoPartition(arr, left, right);

      if (pivot - left < right - pivot) {
        stack.push([pivot + 1, right]);
        right = pivot - 1;
      } else {
        stack.push([left, pivot - 1]);
        left = pivot + 1;
      }
    }
  }
}

function lomutoPartition(arr, left, right) {
  const randomIdx = randomInt(left, right);
  const pivot = arr[randomIdx];
  let wall = left;

  for (let i = left; i < right; i += 1) {
    if (arr[i] <= pivot) {
      swap(arr, i, wall);
      wall += 1;
    }
  }

  swap(arr, right, wall);

  return wall;
}

function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function swap(arr, i, j) {
  if (i === j) return;

  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```

## [Quick Sort 'Randomized Hoare Partition'](https://leetcode.com/problems/sort-an-array/description/)

<!-- notecardId: 1769008183486 -->

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
  const THRESHOLD = 12;
  const n = arr.length;
  if (n < 2) return nums;

  const stack = [[0, n - 1]];

  while (stack.length) {
    let [left, right] = stack.pop();

    if (right - left < THRESHOLD) {
      insertionSort(nums, left, right);

      continue;
    }

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

      if (right - left < THRESHOLD) {
        insertionSort(nums, left, right);

        break;
      }
    }
  }

  return nums;
}

function randomizedPartition(arr, left, right) {
  const randomIdx = randomInt(left, right);
  swap(arr, randomIdx, left);

  return hoarePartition(arr, left, right);
}

function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// [3, 4, 9, 1, 7, 0, 5, 2, 6, 8]

// boundary
// 1) 7
// 2)
// 3)
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

function insertionSort(nums, left, right) {
  for (let i = left + 1; i <= right; i += 1) {
    const current = nums[i];
    if (nums[i - 1] <= current) continue;

    let j = i - 1;

    while (j >= left && nums[j] > current) {
      nums[j + 1] = nums[j];
      j -= 1;
    }

    nums[j + 1] = current;
  }
}

function swap(arr, i, j) {
  if (i === j) return;

  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
