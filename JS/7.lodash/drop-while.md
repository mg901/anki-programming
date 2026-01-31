## [Drop While](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/drop-while)

```js
function dropWhile(array, predicate) {
  let index = 0;

  while (index < array.length && predicate(array[index], index, array)) {
    index += 1;
  }

  return array.slice(index);
}
```
