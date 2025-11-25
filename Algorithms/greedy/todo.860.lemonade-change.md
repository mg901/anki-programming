## [860 Lemonade Change](https://leetcode.com/problems/lemonade-change/description/)

```js
function lemonadeChange(bills) {
  let five = 0;
  let ten = 0;

  for (const bill of bills) {
    if (bill === 5) {
      five += 1;
    } else if (bill === 10) {
      if (five === 0) return false;
      five -= 1;
      ten += 1;
    } else if (ten > 0 && five > 0) {
      ten -= 1;
      five -= 1;
    } else if (five >= 3) {
      five -= 3;
    } else {
      return false;
    }
  }

  return true;
}
```
