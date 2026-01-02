## [1502. Can Make Arithmetic Progression From Sequence](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence/description)

```js
// - Time: O(n)
// - Space: O(n)
function canMakeArithmeticProgression(arr) {
  const n = arr.length;

  let min = arr[0];
  let max = arr[0];

  for (let i = 0; i < n; i += 1) {
    min = Math.min(min, arr[i]);
    max = Math.max(max, arr[i]);
  }

  if (min === max) return true;

  if ((max - min) % (n - 1) !== 0) return false;

  const diff = (max - min) / (n - 1);
  const seen = new Set();

  for (let i = 0; i < n; i += 1) {
    const offset = arr[i] - min;

    if (offset % diff !== 0) return false;

    const pos = offset / diff;
    if (seen.has(pos)) return false;

    seen.add(pos);
  }

  return true;
}
```
