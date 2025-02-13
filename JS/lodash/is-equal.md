## [Is Equal](https://bigfrontend.dev/problem/implement-deep-equal-isEqual)

<!-- notecardId: 1739476543670 -->

```js
function isEqual(x, y) {
  const seenObjects = new WeakMap();

  return traverse(x, y);

  function traverse(a, b) {
    if (a === b) return true;

    const tagA = getTypeTag(a);
    const tagB = getTypeTag(b);

    if (tagA !== tagB) return false;

    if (isPlainObjectOrArray(tagA)) {
      if (seenObjects.has(a) && seenObjects.get(a) === b) return true;
      seenObjects.set(a, b);

      const keysA = Object.keys(a);
      const keysB = Object.keys(b);

      if (keysA.length !== keysB.length) {
        return false;
      }

      for (let i = 0; i < keysA.length; i += 1) {
        const key = keysA[i];

        if (!Object.hasOwn(b, key) || !traverse(a[key], b[key])) {
          return false;
        }
      }

      return true;
    }

    if (Number.isNaN(a) && Number.isNaN(b)) {
      return true;
    }

    return false;
  }
}

function isPlainObjectOrArray(tag) {
  return tag === "[object Object]" || tag === "[object Array]";
}

function getTypeTag(it) {
  return Object.prototype.toString.call(it);
}
```
