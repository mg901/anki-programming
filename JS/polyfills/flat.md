## [Array.prototype.flat](https://bigfrontend.dev/problem/implement-Array-prototype.flat)

<!-- notecardId: 1739882779618 -->

```js
function flat(source, depth = 1) {
  const result = [];
  flattenIntoArray(result, source, 0, depth);

  return result;
}

function flattenIntoArray(target, source, targetIndex, depth) {
  let sourceIdx = 0;

  while (sourceIdx < source.length) {
    const item = source[sourceIdx];

    if (depth > 0 && Array.isArray(item)) {
      targetIndex = flattenIntoArray(target, item, targetIndex, depth - 1);
    } else if (sourceIdx in source) {
      target[targetIndex] = item;
      targetIndex += 1;
    }

    sourceIdx += 1;
  }

  return targetIndex;
}
```
