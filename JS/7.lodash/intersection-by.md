## [IntersectionBy](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/intersection-by)

```js
export default function intersectionBy(iteratee, ...arrays) {
  if (!arrays.length) return [];

  const first = arrays[0];
  const keys = first.map(iteratee);

  let intersection = new Set(keys);

  for (let i = 1; i < arrays.length; i += 1) {
    const set = new Set();

    for (const item of arrays[i]) {
      set.add(iteratee(item));
    }

    intersection = intersection.intersection(set);
    if (intersection.size === 0) return [];
  }

  const seen = new Set();
  const result = [];

  for (let i = 0; i < first.length; i += 1) {
    const key = keys[i];

    if (!seen.has(key) && intersection.has(key)) {
      seen.add(key);
      result.push(first[i]);
    }
  }

  return result;
}
```
