## [intersectionWith](https://www.greatfrontend.com/questions/javascript/intersection-with)

```js
// Algorithm: Vertical Scanning

// - Time: O(m * k * n)
//    where:
//      - m = head.length
//      - k = number of other arrays (tail.length)
//      - n = average size of arrays in tail

// - Space: O(1)
function intersectionWith(comparator, ...arrays) {
  if (arrays.length === 0) return [];

  const [head, ...tail] = arrays;

  return head.filter((item) =>
    tail.every((array) => array.some((value) => comparator(item, value))),
  );
}
```
