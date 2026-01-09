## [Heap Sort](https://leetcode.com/problems/sort-an-array/description)

<!-- notecardId: 1767977502116 -->

```js
// Explanation:
// - Bite Quest: https://youtu.be/ZxH3jcA3EK0
// - Abdul Bari: https://youtu.be/HqPJF2L5h9U

// - Time: O(n log(n))
// - Space: O(1)
function heapSort(nums) {
  const n = nums.length;
  if (n < 2) return nums;

  buildMaxHeap(nums);

  for (let i = n - 1; i > 0; i -= 1) {
    swap(nums, 0, i);
    heapifyDown(nums, 0, i);
  }

  return nums;
}

function buildMaxHeap(nums) {
  const n = nums.length;
  const lastParentIdx = Math.floor(n / 2) - 1;

  for (let i = lastParentIdx; i >= 0; i -= 1) {
    heapifyDown(nums, i, n);
  }
}

function heapifyDown(heap, index, size) {
  while (true) {
    let largestIdx = index;
    let leftChildIdx = index * 2 + 1;
    let rightChildIdx = index * 2 + 2;

    if (leftChildIdx < size && heap[leftChildIdx] > heap[largestIdx]) {
      largestIdx = leftChildIdx;
    }

    if (rightChildIdx < size && heap[rightChildIdx] > heap[largestIdx]) {
      largestIdx = rightChildIdx;
    }

    if (largestIdx === index) break;

    swap(heap, index, largestIdx);
    index = largestIdx;
  }
}

function swap(nums, i, j) {
  if (i === j) return;

  const temp = nums[j];
  nums[j] = nums[i];
  nums[i] = temp;
}
```
