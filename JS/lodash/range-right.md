## [rangeRight](https://www.greatfrontend.com/questions/javascript/range-right)

<!-- notecardId: 1739476563643 -->

```js
function rangeRight(start = 0, end, step = 1) {
  if (end === undefined) {
    end = start;
    start = 0;
  }

  if (end < start && step === 1) {
    step = -1;
  }

  const result = [];
  const length = (end - start) / (step || 1);

  for (let i = 0; i < length; i += 1) {
    result.push(i * step + start);
  }

  return result.reverse();
}
```
