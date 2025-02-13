## [Basic debounce](https://bigfrontend.dev/problem/implement-basic-debounce)

<!-- notecardId: 1739474989716 -->

```js
function debounce(func, wait = 0) {
  let timerId;

  return function debounced(...args) {
    clearTimeout(timerId);

    timerId = setTimeout(() => {
      timerId = undefined;

      func.apply(this, args);
    }, wait);
  };
}
```
