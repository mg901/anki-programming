## [Is Equal](https://bigfrontend.dev/problem/implement-deep-equal-isEqual)

```js
function isEqual(a, b) {
  const seenPairs = new WeakMap();

  return traverse(a, b);

  function traverse(x, y) {
    if (x === y || (Number.isNaN(x) && Number.isNaN(y))) {
      return true;
    }

    if (!isObject(x) || isObject(y)) {
      return false;
    }

    if (seenPairs.has(x) && seenPairs.get(x) === y) {
      return true;
    }

    seenPairs.set(x, y);

    if (Array.isArray(x)) {
      if (x.length !== y.length) return false;

      for (let i = 0; i < x.length; i += 1) {
        if (!traverse(x[i], y[i])) return false;
      }

      return true;
    }

    const keysX = Object.keys(x);
    const keysY = Object.keys(y);

    if (keysX.length !== keysY.length) return false;

    for (const key of keysX) {
      if (!Object.hasOwn(y, key) || !traverse(x[key], y[key])) {
        return false;
      }
    }

    return true;
  }
}

function isObject(it) {
  return it !== null && typeof it === 'object';
}
```
