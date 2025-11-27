## [295 Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/description/)

```js
class MedianFinder {
  #minpq = new MaxPriorityQueue();

  #maxpq = new MinPriorityQueue();

  addNum(num) {
    if (this.#maxpq.isEmpty() || num > this.#maxpq.front()) {
      this.#maxpq.enqueue(num);
    } else {
      this.#minpq.enqueue(num);
    }

    this.#makeBalanced();
  }

  #makeBalanced() {
    if (this.#minpq.size() > this.#maxpq.size()) {
      this.#maxpq.enqueue(this.#minpq.dequeue());
    } else if (this.#maxpq.size() > this.#minpq.size() + 1) {
      this.#minpq.enqueue(this.#maxpq.dequeue());
    }
  }

  findMedian() {
    if (this.#maxpq.size() > this.#minpq.size()) {
      return this.#maxpq.front();
    }

    return (this.#minpq.front() + this.#maxpq.front()) / 2;
  }
}
```
