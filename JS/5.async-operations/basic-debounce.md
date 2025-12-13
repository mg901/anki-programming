## [Basic debounce](https://bigfrontend.dev/problem/implement-basic-debounce)

<!-- notecardId: 1757543923921 -->

```js
function debounce(func, wait = 0) {
  let timerId;

  return function debounced(...args) {
    clearTimeout(timerId);

    timerId = setTimeout(() => {
      func.apply(this, args);
    }, wait);
  };
}
```
