## [Object.assign](https://bigfrontend.dev/problem/implement-object-assign)

```js
function objectAssign(target, ...sources) {
  if (target == null) {
    throw new TypeError('Cannot convert undefined or null to object');
  }

  const to = Object(target);
  if (!sources.length) return to;

  for (const source of sources) {
    if (source == null) continue;

    const from = Object(source);

    const keys = [
      ...Object.keys(from),
      ...Object.getOwnPropertySymbols(from),
    ].filter((key) => Object.prototype.propertyIsEnumerable.call(from, key));

    for (const key of keys) {
      const desc = Object.getOwnPropertyDescriptor(to, key);

      if (desc === undefined || desc.writable === false) {
        to[key] = from[key];
      } else {
        throw new TypeError(`Cannot assign to read-only property '${key}'`);
      }
    }
  }

  return to;
}
```
