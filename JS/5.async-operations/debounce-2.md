## [Debounce 2](https://www.greatfrontend.com/questions/javascript/debounce-ii)

<!-- notecardId: 1739475030934 -->

```js
function debounce(func, wait = 0) {
  let timerId, savedThis, savedArgs;

  function clearTimer() {
    clearTimeout(timerId);
    timerId = undefined;
  }

  function invokeFunc() {
    if (timerId === undefined) return;

    clearTimer();
    func.apply(savedThis, savedArgs);
  }

  function debounced(...args) {
    clearTimer();

    savedThis = this;
    savedArgs = args;

    timerId = setTimeout(() => {
      invokeFunc();
    }, wait);
  }

  debounced.cancel = clearTimer;
  debounced.flush = invokeFunc;

  return debounced;
}
```
