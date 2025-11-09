## [unionBy](https://www.greatfrontend.com/questions/javascript/union-by?language=js)

<!-- notecardId: 1739476575762 -->

```js
function unionBy(iteratee, ...arrays) {
  const visited = new Set();
  const unique = [];

  for (const array of arrays) {
    for (const value of array) {
      const criterion = iteratee(value);

      if (!visited.has(criterion)) {
        visited.add(criterion);
        unique.push(value);
      }
    }
  }

  return unique;
}
```
