## [Promise.any](https://www.greatfrontend.com/questions/javascript/promise-any)

<!-- notecardId: 1739475459327 -->

```js
function promiseAny(iterable) {
  return new Promise((resolve, reject) => {
    const array = Array.from(iterable);
    let rejected = 0;
    let errors = [];
    const error = new AggregateError(errors, "All promises were rejected");

    if (rejected === array.length) {
      reject(error);
    }

    for (let i = 0; i < array.length; i += 1) {
      const item = array[i];

      Promise.resolve(item).then(resolve, (reason) => {
        errors[index] = reason;
        rejected += 1;

        if (rejected === array.length) {
          reject(error);
        }
      });
    }
  });
}
```
