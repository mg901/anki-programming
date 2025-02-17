## [Chunk](https://www.greatfrontend.com/questions/javascript/chunk)

<!-- notecardId: 1739697587549 -->

```js
function chunk(array, size = 1) {
  if (!array.length) return array;

  const result = [];

  for (let i = 0; i < array.length; i += 1) {
    const chunkIndex = Math.floor(i / size);

    if (result[chunkIndex] === undefined) {
      result[chunkIndex] = [];
    }

    result[chunkIndex].push(array[i]);
  }

  return result;
}

// or
function chunk(arr, size) {
  const result = [];

  for (let i = 0; i < arr.length; i += size) {
    result.push(arr.slice(i, i + size));
  }

  return result;
}
```
