## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1768741537226 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/B1k_sxOSgv8

// - Time: O(n)
// - Space: O(n)
function encode(strs) {
  return strs.map((word) => word.length + '#' + word).join('');
}

// - Time: O(n)
// - Space: O(n)
function decode(str) {
  const decoded = [];

  let i = 0;

  while (i < str.length) {
    let delimiterIdx = str.indexOf('#', i);

    const length = str.slice(i, delimiterIdx);
    const start = delimiterIdx + 1;
    const end = start + Number(length);
    const word = str.slice(start, end);
    decoded.push(word);

    i = end;
  }

  return decoded;
}
```
