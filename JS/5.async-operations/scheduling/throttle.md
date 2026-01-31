## [Basic throttle](https://bigfrontend.dev/problem/implement-basic-throttle)

```js
function throttle(func, wait) {
  let isThrottled = false,
    lastThis,
    lastArgs;

  return function throttled(...args) {
    if (isThrottled) {
      lastThis = this;
      lastArgs = args;

      return;
    }

    func.apply(this, args);
    lastThis = lastArgs = undefined;

    isThrottled = true;

    setTimeout(() => {
      isThrottled = false;

      if (lastArgs) {
        throttled.apply(lastThis, lastArgs);
      }
    }, wait);
  };
}
```

## [Throttle with leading & trailing](https://bigfrontend.dev/problem/implement-throttle-with-leading-and-trailing-option)

```js
function throttle(func, wait, { leading = true, trailing = true } = {}) {
  let isThrottled = false,
    lastThis,
    lastArgs;

  return function throttled(...args) {
    if (isThrottled) {
      lastThis = this;
      lastArgs = args;

      return;
    }

    if (leading || lastArgs) {
      func.apply(this, args);
      lastThis = lastArgs = undefined;
    }

    isThrottled = true;

    setTimeout(() => {
      isThrottled = false;

      if (trailing && lastArgs) {
        throttled.apply(lastThis, lastArgs);
      }
    }, wait);
  };
}
```
