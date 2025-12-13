## Is Cyclic

<!-- notecardId: 1739454863461 -->

```js
function isCyclic(value) {
  const seen = new WeakSet();

  return traverse(value);

  function traverse(data) {
    if (data && typeof data === "object") {
      if (seen.has(data)) {
        return true;
      }

      seen.add(data);

      for (const key in data) {
        if (Object.hasOwn(data, key) && traverse(data[key])) {
          return true;
        }
      }
    }

    return false;
  }
}
```
