## [Squash Object](https://www.greatfrontend.com/questions/javascript/squash-object?practice=practice&tab=coding)

```js
function squashObject(obj) {
  const squashed = {};
  traverse(obj, [], squashed);

  return squashed;

  function traverse(o, path, output) {
    for (const key in o) {
      if (!Object.hasOwn(o, key)) continue;

      const value = o[key];
      const fullPath = [...path, key];

      if (value === null || typeof value !== 'object') {
        output[fullPath.filter(Boolean).join('.')] = value;
      } else {
        traverse(value, fullPath, output);
      }
    }
  }
}
```
