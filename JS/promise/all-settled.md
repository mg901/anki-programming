## [Promise.allSettled](https://www.greatfrontend.com/questions/javascript/promise-all-settled)

<!-- notecardId: 1739475449701 -->

```js
function promiseAllSettled(iterable) {
  const array = Array.from(iterable);
  const total = array.length;
  let completed = 0;
  let results = [];

  if (total === 0) {
    return Promise.resolve(results);
  }

  return new Promise((resolve) => {
    for (const [index, item] of array.entries()) {
      Promise.resolve(item)
        .then(
          (value) => {
            results[index] = { value, status: "fulfilled" };
          },
          (reason) => {
            results[index] = { reason, status: "rejected" };
          }
        )
        .finally(() => {
          completed += 1;

          if (completed === total) {
            resolve(results);
          }
        });
    }
  });
}
```
