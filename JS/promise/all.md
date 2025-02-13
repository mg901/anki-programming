## [Promise.all](https://www.greatfrontend.com/interviews/study/javascript-polyfills/questions/javascript/promise-all)

<!-- notecardId: 1739478307911 -->

```js
function promiseAll(iterable) {
  return new Promise((resolve, reject) => {
    const array = Array.from(iterable);
    let resolved = 0;

    if (resolved === array.length) {
      resolve([]);
    }

    for (let i = 0; i < array.length; i += 1) {
      const item = array[i];

      Promise.resolve(item).then((result) => {
        array[index] = result;
        resolved += 1;

        if (resolved === array.length) {
          resolve(array);
        }
      }, reject);
    }
  });
}
```
