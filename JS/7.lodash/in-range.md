## [In Range](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/in-range)

```js
function inRange(value, start, end) {
  if (end === undefined) {
    end = start;
    start = 0;
  }

  if (start > end) {
    const tmp = end;
    end = start;
    start = tmp;
  }

  if (value >= start && value < end) {
    return true;
  }

  return false;
}

// One-liner
function inRange(value, start, end = 0) {
  return Math.min(start, end) <= value && value < Math.max(start, end);
}
```
