## [Promise.finally](https://bigfrontend.dev/problem/implement-Promise-prototype-finally)

<!-- notecardId: 1739475462951 -->

```js
function myFinally(promise, onfinally) {
  const handler = typeof onfinally === "function" ? onfinally : () => onfinally;

  return promise.then(
    (value) => {
      return Promise.resolve(handler()).then(() => value);
    },
    (reason) => {
      return Promise.resolve(handler()).then(() => {
        throw reason;
      });
    }
  );
}
```
