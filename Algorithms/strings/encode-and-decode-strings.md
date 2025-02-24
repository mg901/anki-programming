## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1740329925340 -->

```js
const DELIMITER = "#";

function encode(strings) {
  return strings
    .map((str) => {
      return `${str.length}${DELIMITER}${str}`;
    })
    .join("");
}

function decode(string) {
  const decoded = [];
  let i = 0;

  while (i < string.length) {
    const delimiterIndex = string.indexOf("#", i);
    const length = string[delimiterIndex - 1] - "0";

    const start = delimiterIndex + 1;
    const end = start + length;

    decoded.push(string.slice(start, end));

    i = end;
  }

  return decoded;
}
```
