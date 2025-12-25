## [Heap Sort](https://leetcode.com/problems/sort-an-array/description)

<!-- notecardId: 1766672905873 -->

```js
// Explanation:
// - Bite Quest: https://youtu.be/ZxH3jcA3EK0
// - Abdul Bari: https://youtu.be/HqPJF2L5h9U

// - Time: O(n log(n))
// - Space: O(1)
function heapSort(nums) {
  buildMaxHeap(nums);
  const n = nums.length;

  for (let i = n - 1; i > 0; i -= 1) {
    swap(nums, 0, i);
    heapifyDown(nums, 0, i);
  }

  return nums;
}

function buildMaxHeap(arr) {
  const n = arr.length;
  const lastParentIdx = Math.floor(n / 2) - 1;

  for (let i = lastParentIdx; i >= 0; i -= 1) {
    heapifyDown(arr, i, n);
  }
}

function heapifyDown(arr, index, size) {
  while (true) {
    let largestIdx = index;
    let leftChildIdx = 2 * index + 1;
    let rightChildIdx = 2 * index + 2;

    if (leftChildIdx < size && arr[leftChildIdx] > arr[largestIdx]) {
      largestIdx = leftChildIdx;
    }

    if (rightChildIdx < size && arr[rightChildIdx] > arr[largestIdx]) {
      largestIdx = rightChildIdx;
    }

    if (largestIdx === index) break;

    swap(arr, index, largestIdx);
    index = largestIdx;
  }
}

function swap(arr, i, j) {
  if (i === j) return;

  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
