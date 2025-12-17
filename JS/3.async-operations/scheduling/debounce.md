## [Basic debounce](https://bigfrontend.dev/problem/implement-basic-debounce)

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

## [Debounce with leading & trailing](https://bigfrontend.dev/problem/implement-debounce-with-leading-and-trailing-option)

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
