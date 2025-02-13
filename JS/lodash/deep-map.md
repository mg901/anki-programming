## [Deep Map](https://www.greatfrontend.com/questions/javascript/deep-map?language=js)

<!-- notecardId: 1739476490416 -->

```js
function deepMap(value, fn) {
  const source = value;
  const seen = new WeakMap();

  return traverse(value, fn);

  function traverse(data, func) {
    const isArray = Array.isArray(data);

    if (!isArray && !isPlainObject(data)) {
      return func.call(source, data);
    }

    if (seen.has(data)) {
      return seen.get(data);
    }

    const mapped = isArray ? [] : {};
    seen.set(data, mapped);

    for (const key in data) {
      if (Object.hasOwn(data, key)) {
        mapped[key] = traverse(data[key], fn);
      }
    }

    return mapped;
  }
}

function isPlainObject(it) {
  return Object.prototype.toString.call(it) === "[object Object]";
}
```
