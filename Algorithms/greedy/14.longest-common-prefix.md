## [14 Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description)

```js
function longestCommonPrefix(strs) {
  const n = strs.length;
  if (!n) return '';

  let [prefix] = strs;

  for (let i = 1; i < n; i += 1) {
    while (!strs[i].startsWith(prefix)) {
      prefix = prefix.slice(0, prefix.length - 1);

      if (prefix === '') return '';
    }
  }

  return prefix;
}
```
