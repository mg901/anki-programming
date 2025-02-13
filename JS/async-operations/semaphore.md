## Semaphore

<!-- notecardId: 1739475081755 -->

```js
class Semaphore {
  #limit;

  #count;

  #queue = [];

  constructor(limit) {
    this.#limit = Math.abs(limit);
    this.#count = this.#limit;
  }

  acquire() {
    const { promise, resolve } = Promise.withResolvers();

    if (this.#count > 0) {
      this.#count -= 1;

      resolve();
    } else {
      this.#queue.push(resolve);
    }

    return promise;
  }

  release() {
    if (this.#queue.length > 0) {
      const resolve = this.#queue.shift();

      resolve();
    } else {
      this.#count = Math.min(this.#limit, (this.#count += 1));
    }
  }
}
```
