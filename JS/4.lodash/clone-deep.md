## [Clone Deep](https://bigfrontend.dev/problem/create-cloneDeep)

```js
function cloneDeep(data) {
  const seen = new WeakMap();

  return traverse(data);

  function traverse(it) {
    if (it == null || typeof it !== 'object') {
      return it;
    }

    if (seen.has(it)) {
      return seen.get(it);
    }

    const target = Array.isArray(it)
      ? []
      : Object.create(Object.getPrototypeOf(it));

    seen.set(it, target);

    const keys = [...Object.keys(it), ...Object.getOwnPropertySymbols(it)];

    for (let i = 0; i < keys.length; i += 1) {
      const key = keys[i];
      target[key] = traverse(it[key]);
    }

    return target;
  }
}
```
