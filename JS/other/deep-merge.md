## [Deep Merge](https://www.greatfrontend.com/questions/javascript/deep-merge?language=js)

<!-- notecardId: 1739454845783 -->

```js
function deepMerge(a, b) {
  if (Array.isArray(a) && Array.isArray(b)) {
    return [...a, ...b];
  }

  if (isPlainObject(a) && isPlainObject(b)) {
    const target = Object.assign({}, a);

    for (const key in b) {
      if (Object.hasOwn(b, key)) {
        if (Object.hasOwn(a, key)) {
          target[key] = deepMerge(a[key], b[key]);
        } else {
          target[key] = b[key];
        }
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
