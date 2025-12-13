## [The most frequently occurring character](https://bigfrontend.dev/problem/most-frequently-occurring-character)

```js
// - Time: O(n)
// - Space: O(n)
function count(str) {
  const counter = new Map();
  let result = [];
  let max = 0;

  for (const char of str) {
    counter.set(char, (counter.get(char) ?? 0) + 1);

    if (counter.get(char) > max) {
      result = [];
      max = counter.get(char);
    }

    if (counter.get(char) === max) {
      result.push(char);
    }
  }

  return result.length > 1 ? result : result[0];
}
```
