## [43 Multiply Strings](https://leetcode.com/problems/multiply-strings/description/)

```js
// Explanation
// - Neetcode: https://youtu.be/1vZswirL8Y8

// - Time: O(m * n)
// - Space: O(m + n)
function multiply(num1, num2) {
  if (num1 === '0' || num2 === '0') return '0';

  const m = num1.length;
  const n = num2.length;
  const RADIX = 10;
  const codeZero = '0'.codePointAt(0);
  const product = new Uint32Array(m + n);

  for (let i = m - 1; i >= 0; i -= 1) {
    for (let j = n - 1; j >= 0; j -= 1) {
      const digit1 = num1.codePointAt(i) - codeZero;
      const digit2 = num2.codePointAt(j) - codeZero;

      const value = product[i + j + 1] + digit1 * digit2;
      product[i + j + 1] = value % RADIX;
      product[i + j] += (value / RADIX) ^ 0;
    }
  }

  let start = 0;
  while (product[start] === 0) {
    start += 1;
  }

  return product.slice(start).join('');
}
```
