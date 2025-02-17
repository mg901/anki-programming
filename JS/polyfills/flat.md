## [Array.prototype.flat](https://bigfrontend.dev/problem/implement-Array-prototype.flat)

<!-- notecardId: 1739803362888 -->

```js
function flat(source, depth = 1) {
  const result = [];
  flattenIntoArray(result, source, source.length, 0, depth);

  return result;
}

function flattenIntoArray(target, source, sourceLen, start, depth) {
  let targetIndex = start;
  let sourceIndex = 0;

  while (sourceIndex < sourceLen) {
    const element = source[sourceIndex];

    if (depth > 0 && Array.isArray(element)) {
      targetIndex = flattenIntoArray(
        target,
        element,
        element.length,
        targetIndex,
        depth - 1
      );
    } else if (sourceIndex in source) {
      target[targetIndex] = element;
      targetIndex += 1;
    }

    sourceIndex += 1;
  }

  return targetIndex;
}
```
