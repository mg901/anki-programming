## [763 Partition Labels](https://leetcode.com/problems/partition-labels/description/)

```js
// Explanation:
// - Neetcode:

// - Time: O(n)
// - Space: O(1)
function partitionLabels(s) {
  const n = s.length;
  const ALPHABET_SIZE = 26;
  const codeA = 'a'.codePointAt(0);
  const lastIndexes = new Uint8Array(ALPHABET_SIZE);

  for (let i = 0; i < n; i += 1) {
    lastIndexes[s.codePointAt(i) - codeA] = i;
  }

  const result = [];
  let size = 0;
  let end = 0;

  for (let i = 0; i < n; i += 1) {
    size += 1;
    end = Math.max(end, lastIndexes[s.codePointAt(i) - codeA]);

    if (i === end) {
      result.push(size);
      size = 0;
    }
  }

  return result;
}
```
