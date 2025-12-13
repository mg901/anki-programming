## [Set](https://bigfrontend.dev/problem/lodash-set)

<!-- notecardId: 1739476571539 -->

```js
function set(source, path, value) {
  if (source == null || !path.length) {
    return source;
  }

  if (typeof path === "string") {
    path = pathToArray(path);
  }

  let current = source;

  for (let i = 0; i < path.length; i += 1) {
    const key = path[i];
    const isLastKey = key === path.at(-1);

    if (isLastKey) {
      current[key] = value;
    } else {
      if (!Object.hasOwn(current, key)) {
        const nextKey = path[i + 1];
        const isNextKeyNumeric = /^(0|[1-9]\d*)$/.test(nextKey);

        current[key] = isNextKeyNumeric ? [] : {};
      }

      current = current[key];
    }
  }

  return source;
}

function pathToArray(path) {
  return path.replace(/\[(\d+)\]/g, ".$1").split(".");
}
```
