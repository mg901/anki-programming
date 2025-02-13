## [maxBy](https://www.greatfrontend.com/questions/javascript/max-by)

<!-- notecardId: 1739476586415 -->

```js
function maxBy(array, iteratee) {
  let max;
  let result;

  for (const item of array) {
    const current = iteratee(item);

    if ((current != null && max === undefined) || current > max) {
      max = current;
      result = item;
    }
  }

  return result;
}
```
