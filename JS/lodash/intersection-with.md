## [intersectionWith](https://www.greatfrontend.com/questions/javascript/intersection-with)

<!-- notecardId: 1739476531317 -->

[#intersection]()

```js
function intersectionWith(comparator, ...arrays) {
  if (arrays.length === 0) return [];

  const [head, ...tail] = arrays;

  return head.filter((item) =>
    tail.every((array) => array.some((value) => comparator(item, value)))
  );
}
```
