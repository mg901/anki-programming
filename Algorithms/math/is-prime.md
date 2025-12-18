## [Is Prime](https://bigfrontend.dev/problem/isPrime)

<!-- notecardId: 1766008611524 -->

```js
// - Time: O()
// - Space: O(1)
function isPrime(num) {
  if (num === 1) return false;

  const limit = Math.sqrt(num);

  for (let i = 2; i <= limit; i += 1) {
    // A number is prime if it is not divisible by any integer in [2, √n].
    if (num % i === 0) {
      return false;
    }
  }

  return true;
}
```
