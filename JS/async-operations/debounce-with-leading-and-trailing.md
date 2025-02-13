## [Debounce with leading & trailing](https://bigfrontend.dev/problem/implement-debounce-with-leading-and-trailing-option)

<!-- notecardId: 1739475034586 -->

```js
function debounce(func, wait = 0, { leading = false, trailing = true } = {}) {
  let timerId, lastThis, lastArgs;

  function invokeFunc() {
    func.apply(lastThis, lastArgs);
    lastThis = lastArgs = undefined;
  }

  function startTimer() {
    timerId = setTimeout(() => {
      timerId = undefined;

      if (trailing && lastArgs) {
        invokeFunc();
      }
    }, wait);
  }

  return function debounced(...args) {
    lastThis = this;
    lastArgs = args;

    if (timerId === undefined) {
      if (leading) {
        invokeFunc();
      }

      startTimer();
    } else {
      clearTimeout(timerId);
      startTimer();
    }
  };
}
```
