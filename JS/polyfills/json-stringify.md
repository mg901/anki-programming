## [JSON.stringify](https://www.greatfrontend.com/interviews/study/javascript-polyfills/questions/javascript/json-stringify)

<!-- notecardId: 1739475852301 -->

```js
function jsonStringify(data) {
  if (data === null) {
    return "null";
  }

  if (Array.isArray(data)) {
    return `[${data.map(jsonStringify)}]`;
  }

  if (typeof data === "object") {
    const result = [];

    for (const key in data) {
      if (Object.hasOwn(data, key)) {
        result.push(`"${key}":${jsonStringify(data[key])}`);
      }
    }

    return `{${result.join(",")}}`;
  }

  if (typeof data === "string") {
    return `"${data}"`;
  }

  return String(data);
}
```
