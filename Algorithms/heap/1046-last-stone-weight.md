## [1046 Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/)

<!-- notecardId: 1743519896267 -->

```js
function lastStoneWeight(stones) {
  const maxHeap = new MaxHeap();

  stones.forEach((stone) => maxHeap.insert(stone));

  while (maxHeap.size > 1) {
    const a = maxHeap.poll();
    const b = maxHeap.poll();
    const diff = a - b;

    if (diff > 0) {
      maxHeap.insert(diff);
    }
  }

  return maxHeap.peek() ?? 0;
}

class MaxHeap {
  #compare;

  #nodes;

  constructor(
    compare = (a, b) => {
      if (a === b) return 0;

      return a > b ? 1 : -1;
    }
  ) {
    this.#compare = compare;
    this.#nodes = [];
  }

  get size() {
    return this.#nodes.length;
  }

  get isEmpty() {
    return this.#nodes.length === 0;
  }

  peek() {
    return this.#nodes[0] ?? null;
  }

  insert(value) {
    this.#nodes.push(value);
    this.#heapifyUp(this.size - 1);

    return this;
  }

  #heapifyUp(index) {
    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);

      if (this.#isPrior(parentIndex, index)) break;
      this.#swap(index, parentIndex);

      index = parentIndex;
    }
  }

  #isPrior(i, j) {
    return this.#compare(this.#nodes[i], this.#nodes[j]) > 0;
  }

  #swap(i, j) {
    const temp = this.#nodes[j];
    this.#nodes[j] = this.#nodes[i];
    this.#nodes[i] = temp;
  }

  poll() {
    if (this.#nodes.length === 0) return null;
    if (this.#nodes.length === 1) return this.#nodes.pop();

    const min = this.#nodes[0];
    this.#nodes[0] = this.#nodes.pop();
    this.#heapifyDown(0);

    return min;
  }

  #heapifyDown(index) {
    while (true) {
      let largestIdx = index;
      let leftChildIdx = index * 2 + 1;
      let rightChildIdx = index * 2 + 2;

      if (leftChildIdx < this.size && this.#isPrior(leftChildIdx, largestIdx)) {
        largestIdx = leftChildIdx;
      }

      if (
        rightChildIdx < this.size &&
        this.#isPrior(rightChildIdx, largestIdx)
      ) {
        largestIdx = rightChildIdx;
      }

      if (largestIdx === index) break;

      this.#swap(index, largestIdx);

      index = largestIdx;
    }
  }

  toArray() {
    return Array.from(this.#nodes);
  }
}
```
