## [Deep Merge](https://www.greatfrontend.com/questions/javascript/deep-merge?language=js)

<!-- notecardId: 1739880566356 -->

```js
function deepMerge(a, b) {
  if (Array.isArray(a) && Array.isArray(b)) {
    return [...a, ...b];
  }

  if (isPlainObject(a) && isPlainObject(b)) {
    const target = { ...a };

    for (const bKey in b) {
      if (!Object.hasOwn(b, bKey)) continue;

      if (Object.hasOwn(a, bKey)) {
        target[bKey] = deepMerge(a[bKey], b[bKey]);
      } else {
        target[bKey] = b[bKey];
      }
    }

    return target;
  }

  return b;
}

function isPlainObject(it) {
  return Object.prototype.toString.call(it) === "[object Object]";
}
```
