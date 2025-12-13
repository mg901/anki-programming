## [Deep Map](https://www.greatfrontend.com/questions/javascript/deep-map?language=js)

<!-- notecardId: 1739880295101 -->

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

    const target = isArray ? [] : {};
    seen.set(data, target);

    for (const key in data) {
      if (Object.hasOwn(data, key)) {
        target[key] = traverse(data[key], fn);
      }
    }

    return target;
  }
}

function isPlainObject(it) {
  return Object.prototype.toString.call(it) === "[object Object]";
}
```
