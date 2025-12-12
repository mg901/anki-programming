## [Heap Sort](https://www.greatfrontend.com/questions/algo/heap-sort)

```js
// Explanation:
// - Bite Quest: https://youtu.be/ZxH3jcA3EK0
// - Abdul Bari: https://youtu.be/HqPJF2L5h9U

// - Time: O(n log(n))
// - Space: O(1)
function heapSort(arr) {
  buildMaxHeap(arr);

  for (let i = arr.length - 1; i > 0; i -= 1) {
    swap(arr, 0, i);
    heapifyDown(arr, 0, i);
  }

  return arr;
}

function buildMaxHeap(arr) {
  const n = arr.length;

  for (let i = Math.floor(n / 2) - 1; i >= 0; i -= 1) {
    heapifyDown(arr, i, n);
  }
}

function heapifyDown(arr, i, heapSize) {
  while (true) {
    let largest = i;
    const leftChild = i * 2 + 1;
    const rightChild = i * 2 + 2;

    if (leftChild < heapSize && arr[leftChild] > arr[largest]) {
      largest = leftChild;
    }

    if (rightChild < heapSize && arr[rightChild] > arr[largest]) {
      largest = rightChild;
    }

    if (largest === i) break;

    swap(arr, i, largest);
    i = largest;
  }
}

function swap(arr, i, j) {
  const temp = arr[j];
  arr[j] = arr[i];
  arr[i] = temp;
}
```
