# [405 Convert a Number to Hexadecimal](https://leetcode.com/problems/convert-a-number-to-hexadecimal/description/)

```js
// - Time: O(n)
// - Space: O(1)
function toHex(num) {
  if (num === 0) return '0';

  const hexChars = '0123456789abcdef';
  let result = '';

  let n = num >>> 0; // to unsigned 32 bit integer

  while (n > 0) {
    const remainder = n % 16;
    result = hexChars[remainder] + result;
    n = Math.floor(n / 16);
  }

  return result;
}
```
