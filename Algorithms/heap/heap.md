## [Max Heap](https://www.greatfrontend.com/questions/algo/heap)

<!-- notecardId: 1766683224218 -->

```js
// Explanation:
// - Abdul Bari: https://youtu.be/HqPJF2L5h9U

export default class Heap {
  #items;

  constructor(array = []) {
    this.#items = [];
    this.heapify(array);
  }

  get size() {
    return this.#items.length;
  }

  // - Time: O(n)
  heapify(array) {
    this.#items = array;
    const lastParentIdx = Math.floor(this.size / 2) - 1;

    for (let i = lastParentIdx; i >= 0; i -= 1) {
      this.#heapifyDown(i);
    }
  }

  // - Time: O(log(n))
  #heapifyDown(index) {
    while (true) {
      let largestIdx = index;
      let leftChildIdx = 2 * index + 1;
      let rightChildIdx = 2 * index + 2;

      if (
        leftChildIdx < this.size &&
        this.#items[leftChildIdx] > this.#items[largestIdx]
      ) {
        largestIdx = leftChildIdx;
      }

      if (
        rightChildIdx < this.size &&
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
    this.#heapifyUp(this.size - 1);
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
    const items = this.#items;

    if (this.size === 0) return undefined;
    if (this.size === 1) return items.pop();

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
