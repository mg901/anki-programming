## [intersection](https://www.greatfrontend.com/interviews/study/lodash/questions/javascript/intersection)

```js
// - Time: O(∑ |arrays[i]|)
// - Space: O(∑ |arrays[i]|)
function intersection(...arrays) {
  const k = arrays.length;

  if (k === 0) return [];
  if (k === 1) return [...new Set(arrays[0])]; // O(n)

  const head = arrays[0];
  const sets = [];

  // O(k - 1)
  for (let i = 1; i < k; i += 1) {
    const set = new Set(arrays[i]); // O((k - 1) * n)

    if (set.size === 0) return []; // Short-circuit

    sets.push(set); // O(1)
  }

  const result = [];
  const seen = new Set();

  for (const val of head) {
    if (seen.has(val)) continue; // O(1)

    let isCommon = true;

    for (const set of sets) {
      if (!set.has(val)) {
        // O(1)
        isCommon = false;
        break;
      }
    }

    if (isCommon) {
      result.push(val); // O(1)
      seen.add(val); // O(1)
    }
  }

  return result;
}
```
