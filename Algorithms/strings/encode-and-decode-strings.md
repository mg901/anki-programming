## [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

<!-- notecardId: 1740850336189 -->

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

  while (i < str.length) {
    let delimiterIndex = str.indexOf("#", i);
    let length = str.slice(i, delimiterIndex) - "0";
    const start = delimiterIndex + 1;
    const end = start + length;
    decoded.push(str.slice(start, end));
    i = end;
  }

  return decoded;
}
```
