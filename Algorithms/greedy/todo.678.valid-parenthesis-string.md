## [678 Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/description/)

```js
function checkValidString(str) {
  let openMin = 0;
  let openMax = 0;

  for (const char of str) {
    if (char === '(') {
      openMin += 1;
      openMax += 1;
    } else if (char === ')') {
      openMin -= 1;
      openMax -= 1;
    } else {
      openMin -= 1;
      openMax += 1;
    }

    if (openMax < 0) return false;
    if (openMin < 0) openMin = 0;
  }

  return openMin === 0;
}
```
