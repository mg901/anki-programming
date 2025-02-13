## [The most frequently occurring character](https://bigfrontend.dev/problem/most-frequently-occurring-character)

<!-- notecardId: 1739454890811 -->

```js
function count(str) {
  if (!str.length) return str;

  const map = new Map();

  for (const char of str) {
    map.set(char, (map.get(char) ?? 0) + 1);
  }

  const max = Math.max(...map.values());
  const result = [];

  for (const [key, freq] of map) {
    if (freq === max) {
      result.push(key);
    }
  }

  return result.length === 1 ? result.at(0) : result;
}
```
