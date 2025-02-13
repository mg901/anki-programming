## [Clone Deep](https://bigfrontend.dev/problem/create-cloneDeep)

<!-- notecardId: 1739476471131 -->

```js
function cloneDeep(data) {
  const seen = new WeakMap();

  return traverse(data);

  function traverse(it) {
    if (it == null || typeof it !== "object") {
      return it;
    }

    if (seen.has(it)) {
      return seen.get(it);
    }

    const clone = Array.isArray(it) ? [] : {};
    seen.set(it, clone);

    const enumerableSymbolKeys = Object.getOwnPropertySymbols(it).filter(
      (prop) => Object.prototype.propertyIsEnumerable.call(it, prop)
    );

    const keys = [...Object.keys(it), ...enumerableSymbolKeys];

    for (let i = 0; i < keys.length; i += 1) {
      const key = keys[i];
      clone[key] = traverse(it[key]);
    }

    return clone;
  }
}
```
