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
  const result = new Uint32Array(m + n);

  for (let i = m - 1; i >= 0; i -= 1) {
    for (let j = n - 1; j >= 0; j -= 1) {
      const digit1 = +num1[i];
      const digit2 = +num2[j];

      const value = result[i + j + 1] + digit1 * digit2;
      result[i + j + 1] = value % RADIX;
      result[i + j] += (value / RADIX) ^ 0;
    }
  }

  let start = 0;
  while (result[start] === 0) start += 1;

  return result.slice(start).join('');
}
```
