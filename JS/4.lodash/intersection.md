## [intersection](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/intersection)

```js
// Old-fashioned solution
function intersection(...arrays) {
  if (!arrays.length) return [];

  const set = new Set(arrays.at(0));

  for (let i = 1; i < arrays.length; i += 1) {
    const array = arrays[i];

    set.forEach((value) => {
      if (!array.includes(value)) {
        set.delete(value);
      }
    });
  }

  return Array.from(set);
}

// Modern solution
function intersection(...arrays) {
  const firstSet = new Set(arrays.at(0));
  const otherSets = arrays.slice(1).map((array) => new Set(array));

  let intersections = firstSet;

  for (const set of otherSets) {
    intersections = intersections.intersection(set);
    if (intersections.size === 0) return [];
  }

  return Array.from(intersections);
}
```
