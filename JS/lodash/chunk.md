## [Chunk](https://www.greatfrontend.com/questions/javascript/chunk)

<!-- notecardId: 1739697587549 -->

```js
export default function chunk(array, size = 1) {
  if (!array.length) return array;

  return array.reduce((acc, item, index) => {
    const idx = Math.floor(index / size);

    (acc[idx] ??= []).push(item);

    return acc;
  }, []);
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
