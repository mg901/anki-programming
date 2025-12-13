## [Array.prototype.flat](https://bigfrontend.dev/problem/implement-Array-prototype.flat)

<!-- notecardId: 1739882779618 -->

```js
function flat(source, depth = 1) {
  const result = [];
  flatten(source, depth);

  return result;

  function flatten(source, depth) {
    for (const item of source) {
      if (depth > 0 && Array.isArray(item)) {
        flatten(item, depth - 1);
      } else {
        result.push(item);
      }
    }
  }
}
```
