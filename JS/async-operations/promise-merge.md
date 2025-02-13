## [Promise Merge](https://www.greatfrontend.com/interviews/study/async-operations/questions/javascript/promise-merge)

<!-- notecardId: 1739475049482 -->

```js
export default function promiseMerge(p1, p2) {
  return Promise.all([p1, p2]).then(([a, b]) => {
    const tagA = tag(a);
    const tagB = tag(b);
    const reason = new TypeError("Unsupported data types");

    if (tagA !== tagB) {
      throw reason;
    }

    switch (tagA) {
      case "String":
      case "Number":
        return a + b;
      case "Array":
        return [...a, ...b];
      case "Object":
        return { ...a, ...b };
      default:
        throw reason;
    }
  });
}

function tag(it) {
  return Object.prototype.toString.call(it).slice(8, -1);
}
```
