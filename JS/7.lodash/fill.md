## [Fill](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/fill)

```js
function fill(array, value, start = 0, end = array.length) {
  const n = array.length;

  start = Math.max(0, start < 0 ? n + start : start);
  end = Math.min(n, end < 0 ? n + end : end);

  for (let i = start; i < end; i += 1) {
    array[i] = value;
  }

  return array;
}
```
