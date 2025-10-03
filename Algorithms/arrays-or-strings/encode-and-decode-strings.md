## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1759145526816 -->

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
    let j = i;
    while (str[j] !== '#') {
      j += 1;
    }

    const length = str.slice(i, j);
    const start = j + 1;
    const end = start + Number(length);
    const word = str.slice(start, end);
    decoded.push(word);

    i = end;
  }

  return decoded;
}
```
