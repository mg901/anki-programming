## [Deep Map](https://www.greatfrontend.com/questions/javascript/deep-map?language=js)

```js
function deepMap(value, fn) {
  const source = value;
  const seen = new WeakMap();

  return traverse(value, fn);

  function traverse(data, func) {
    const isArray = Array.isArray(data);

    if (!isArray && !isObjectLike(data)) {
      return func.call(source, data);
    }

    if (seen.has(data)) {
      return seen.get(data);
    }

    const target = isArray ? [] : {};
    seen.set(data, target);

    const keys = [...Object.keys(data), ...Object.getOwnPropertySymbols(data)];

    for (const key of keys) {
      target[key] = traverse(data[key], func);
    }

    return target;
  }
}

function isObjectLike(it) {
  return Object.prototype.toString.call(it) === '[object Object]';
}
```
