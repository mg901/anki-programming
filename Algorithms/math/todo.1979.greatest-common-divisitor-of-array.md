## [1979 Find Greatest Common Divisor of Array](https://leetcode.com/problems/find-greatest-common-divisor-of-array/description/)

```js
// - Time: O(n + log(min(a, b)))
// - Space: O(1)
function findGCD(nums) {
  const a = Math.min(...nums);
  const b = Math.max(...nums);

  return gcd(a, b);
}

// - Time: O(log(min(a, b)))
// - Space: O(1)
function gcd(a, b) {
  while (b !== 0) {
    let temp = b;
    b = a % b;
    a = temp;
  }

  return a;
}
```
