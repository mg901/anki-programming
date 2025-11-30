## [69 Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/zdMhGxRWutQ

// - Time: O(log(n))
// - Space: O(1)
function mySqrt(x) {
  let left = 1;
  let right = (x >> 1) + 1;

  while (left <= right) {
    const mid = left + ((right - left) >> 1);

    if (mid * mid === x) return mid;

    if (mid * mid > x) {
      right = mid - 1;
    } else {
      left = mid + 1;
    }
  }

  return right;
}
```
