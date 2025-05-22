## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1747405053362 -->

```js
function encode(strings) {
  let encoded = '';

  for (const word of strs) {
    encoded += `${word.length}#${word}`;
  }

  return encoded;
}

function decode(string) {
  const decoded = [];

  let i = 0;

  while (i < str.length) {
    const delimiterIndex = str.indexOf('#', i);
    const length = str.slice(i, delimiterIndex);

    const start = delimiterIndex + 1;
    const end = start + Number(length);
    const word = str.slice(start, end);

    decoded.push(word);

    i = end;
  }

  return decoded;
}
```
