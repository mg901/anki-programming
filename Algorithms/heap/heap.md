## [Max Heap](https://www.greatfrontend.com/questions/algo/heap)

<!-- notecardId: 1766669429664 -->

```js
// Explanation:
// - Abdul Bari: https://youtu.be/HqPJF2L5h9U

class Heap {
  #items;

  constructor(array = []) {
    this.#items = [];
    this.heapify(array);
  }

  // - Time: O(n)
  heapify(array) {
    this.#items = array;
    const size = this.#items.length;
    const lastParentIdx = Math.floor(size / 2) - 1;

    for (let i = lastParentIdx; i >= 0; i -= 1) {
      this.#heapifyDown(i);
    }
  }

  // - Time: O(log(n))
  #heapifyDown(index) {
    const size = this.#items.length;

    while (true) {
      let largestIdx = index;
      let leftChildIdx = 2 * index + 1;
      let rightChildIdx = 2 * index + 2;

      if (
        leftChildIdx < size &&
        this.#items[leftChildIdx] > this.#items[largestIdx]
      ) {
        largestIdx = leftChildIdx;
      }

      if (
        rightChildIdx < size &&
        this.#items[rightChildIdx] > this.#items[largestIdx]
      ) {
        largestIdx = rightChildIdx;
      }

      if (largestIdx === index) break;

      this.#swap(index, largestIdx);
      index = largestIdx;
    }
  }

  // - Time: O(log(n))
  insert(value) {
    this.#items.push(value);
    this.#heapifyUp(this.#items.length - 1);
  }

  // - Time: O(log(n))
  #heapifyUp(index) {
    const items = this.#items;

    while (index > 0) {
      const parentIdx = Math.floor((index - 1) / 2);

      if (items[parentIdx] >= items[index]) break;

      this.#swap(index, parentIdx);
      index = parentIdx;
    }
  }

  // - Time: O(log(n))
  delete() {
    const size = this.#items.length;
    const items = this.#items;

    if (size === 0) return undefined;
    if (size === 1) return items.pop();

    const max = items[0];
    items[0] = items.pop();
    this.#heapifyDown(0);

    return max;
  }

  findMax() {
    return this.#items[0];
  }

  #swap(i, j) {
    if (i === j) return;

    const items = this.#items;
    const temp = items[j];

    items[j] = items[i];
    items[i] = temp;
  }
}
```
