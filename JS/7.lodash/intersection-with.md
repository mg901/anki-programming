## [intersectionWith](https://www.greatfrontend.com/questions/javascript/intersection-with)

```js
// Algorithm: Vertical Scanning

// - Time: O(n * k * m)
//    where:
//      - n = head.length
//      - k = number of other arrays (tail.length)
//      - m = average size of arrays in tail

// - Space: O(1)
function intersectionWith(comparator, ...arrays) {
  const k = arrays.length;

  if (k === 0) return [];
  if (k === 1) return [...arrays[0]];

  const [head, ...tail] = arrays;

  return head.filter((val) =>
    tail.every((array) => array.some((otherVal) => comparator(val, otherVal))),
  );
}
```
