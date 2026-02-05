## [Deep Merge](https://www.greatfrontend.com/questions/javascript/deep-merge?language=js)

```js
function deepMerge(a, b) {
  if (Array.isArray(a) && Array.isArray(b)) {
    return [...a, ...b];
  }

  if (isObjectLike(a) && isObjectLike(b)) {
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

function isObjectLike(it) {
  return Object.prototype.toString.call(it) === '[object Object]';
}
```
