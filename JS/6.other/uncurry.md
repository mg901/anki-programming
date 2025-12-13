## Uncurry

<!-- notecardId: 1739454894540 -->

```js
function uncurry(func) {
  return function (...args) {
    if (!args.length) return func;

    let result = func;

    for (const arg of args) {
      if (typeof result !== "function") break;

      result = result(arg);
    }

    return result;
  };
}
```
