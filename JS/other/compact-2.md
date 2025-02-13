## [Compact 2](https://www.greatfrontend.com/questions/javascript/compact-ii?language=js)

<!-- notecardId: 1739454815939 -->

```js
function compact(data) {
  if (!data || typeof data !== "object") return data;

  if (Array.isArray(data)) {
    const newArray = [];

    for (let i = 0; i < data.length; i += 1) {
      if (data[i]) {
        newArray.push(data[i]);
      }
    }

    return newArray;
  }

  const obj = {};

  for (const key in data) {
    if (Object.hasOwn(data, key) && data[key]) {
      const value = compact(data[key]);

      obj[key] = value;
    }
  }

  return obj;
}
```
