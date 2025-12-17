## [Complete Assign](https://bigfrontend.dev/problem/implement-completeAssign)

```js
function completeAssign(target, ...sources) {
  let to = target;
  if (to == null) {
    throw new TypeError('Cannot convert undefined or null to object');
  }

  to = Object(to);
  if (!sources.length) return to;

  for (const source of sources) {
    if (source == null) continue;

    Object.defineProperties(to, Object.getOwnPropertyDescriptors(source));
  }

  return to;
}
```
