## [Deep Omit](https://www.greatfrontend.com/questions/javascript/deep-omit?language=js)

<!-- notecardId: 1739478148185 -->

```js
function deepOmit(value, keys) {
  const seen = new WeakMap();

  return traverse(value, keys);

  function traverse(data, omitKeys) {
    if (!keys.length || (!Array.isArray(data) && !isPlainObject(data))) {
      return data;
    }

    if (seen.has(data)) {
      return seen.get(data);
    }

    const target = Array.isArray(data) ? [] : {};
    seen.set(data, target);

    for (const key in data) {
      if (!Object.hasOwn(data, key)) continue;

      if (!keys.includes(key)) {
        target[key] = traverse(data[key], omitKeys);
      }
    }

    return target;
  }
}

function isPlainObject(it) {
  return Object.prototype.toString.call(it) === "[object Object]";
}
```
