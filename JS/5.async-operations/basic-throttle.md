## [Basic throttle](https://bigfrontend.dev/problem/implement-basic-throttle)

<!-- notecardId: 1739474992990 -->

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
