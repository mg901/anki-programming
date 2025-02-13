## [IntersectionBy](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/intersection-by)

<!-- notecardId: 1739476525240 -->

[#intersection]()

```js
function intersectionBy(iteratee, ...arrays) {
  if (!arrays.length) return [];

  const first = arrays.at(0);
  const mappedFirst = first.map(iteratee);

  const otherSets = arrays
    .slice(1)
    .map((array) => new Set(array.map(iteratee)));

  let intersections = new Set(mappedFirst);

  for (const set of otherSets) {
    intersections = intersections.intersection(set);
    if (intersections.size === 0) return [];
  }

  const seen = new Set();
  const result = [];

  for (let i = 0; i < first.length; i += 1) {
    const value = mappedFirst[i];

    if (!seen.has(value) && intersections.has(value)) {
      seen.add(value);
      result.push(first[i]);
    }
  }

  return result;
}
```
