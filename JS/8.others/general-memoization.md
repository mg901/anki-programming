## [General momoization function](https://bigfrontend.dev/problem/implement-general-memoization-function)

```js
function memo(func, resolver = (...args) => args.join('_')) {
  const cache = new Map();

  return function (...args) {
    const key = resolver(...args);

    if (!cache.has(key)) {
      cache.set(key, func.apply(this, args));
    }

    return cache.get(key);
  };
}
```
