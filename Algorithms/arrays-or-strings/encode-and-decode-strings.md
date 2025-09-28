## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1759008509785 -->

```js
// Explanation:
// - Neetcode: https://youtu.be/B1k_sxOSgv8

// - Time: O(n)
// - Space: O(n)
function encode(strs) {
  let encoded = [];

  for (const word of strs) {
    encoded.push(`${word.length}#${word}`);
  }

  return encoded.join('');
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
