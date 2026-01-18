## [763 Partition Labels](https://leetcode.com/problems/partition-labels/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/B7m8UmZE-vw

// - Time: O(n)
// - Space: O(1)
function partitionLabels(s) {
  const n = s.length;
  const lastIndexes = {};
  const result = [];

  for (let i = 0; i < n; i += 1) {
    lastIndexes[s[i]] = i;
  }

  let start = 0;
  let end = 0;

  for (let i = 0; i < n; i += 1) {
    end = Math.max(end, lastIndexes[s[i]]);

    if (i === end) {
      result.push(end - start + 1);
      start = i + 1;
    }
  }

  return result;
}
```
