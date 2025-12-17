## [Deep Clone 2](https://www.greatfrontend.com/questions/javascript/deep-clone-ii?language=js)

```js
function deepClone(value) {
  const seen = new WeakMap();

  return traverse(value);

  function traverse(data) {
    if (data == null || typeof data !== 'object') {
      return data;
    }

    if (seen.has(data)) {
      return seen.get(data);
    }

    if (data instanceof Date) {
      return new Date(data);
    }

    if (data instanceof RegExp) {
      return new RegExp(data);
    }

    if (Array.isArray(data)) {
      return data.map(deepClone);
    }

    const target = Object.create(Object.getPrototypeOf(data));
    seen.set(data, target);

    const keys = [...Object.keys(data), ...Object.getOwnPropertySymbols(data)];

    for (const key of keys) {
      target[key] = traverse(data[key], seen);
    }

    return target;
  }
}
```
