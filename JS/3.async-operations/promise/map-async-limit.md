## [Map Async Limit 'semaphore'](https://www.greatfrontend.com/interviews/study/async-operations/questions/javascript/map-async-limit)

```js
class Semaphore {
  #queue = [];

  #limit;

  constructor(limit) {
    this.#limit = Math.abs(limit);
  }

  acquire() {
    const { promise, resolve } = Promise.withResolvers();

    if (this.#limit > 0) {
      this.#limit -= 1;

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
    }
  }
}

function mapAsyncLimit(iterable, callbackFn, size = Infinity) {
  const results = [];
  const { length } = iterable;

  const limit = Math.min(length, size);
  const semaphore = new Semaphore(limit);
  const promises = [];

  for (let index = 0; index < length; index += 1) {
    promises.push(
      semaphore.acquire().then(() =>
        callbackFn(iterable[index])
          .then((value) => {
            results[index] = value;
          })
          .finally(() => {
            semaphore.release();
          }),
      ),
    );
  }

  return Promise.all(promises).then(() => results);
}
```
