## [Array.prototype.flat](https://bigfrontend.dev/problem/implement-Array-prototype.flat)

<!-- notecardId: 1739882779618 -->

```js
function flat(source, depth = 1) {
  const result = [];
  flattenIntoArray(result, source, 0, depth);

  return result;
}

function flattenIntoArray(target, source, targetIndex, depth) {
  let sourceIndex = 0;

  while (sourceIndex < source.length) {
    const item = source[sourceIndex];

    if (depth > 0 && Array.isArray(item)) {
      targetIndex = flattenIntoArray(target, item, targetIndex, depth - 1);
    } else if (sourceIndex in source) {
      target[targetIndex] = item;
      targetIndex += 1;
    }

    sourceIndex += 1;
  }

  return targetIndex;
}
```
