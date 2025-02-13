## [Get](https://www.greatfrontend.com/questions/javascript/get)

<!-- notecardId: 1739476510896 -->

```js
function get(source, path, defaultValue) {
  if (source == null || !path.length) {
    return defaultValue;
  }

  if (typeof path === "string") {
    path = pathToArray(path);
  }

  let current = source;

  for (const step of path) {
    if (current && Object.hasOwn(current, step)) {
      current = current[step];
    } else {
      return defaultValue;
    }
  }

  return current;
}

function pathToArray(path) {
  return path.replace(/\[(\d+)\]/g, ".$1").split(".");
}
```
