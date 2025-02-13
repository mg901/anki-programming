## [Is Prime](https://bigfrontend.dev/problem/isPrime)

<!-- notecardId: 1739477225437 -->

```js
function isPrime(num) {
  if (num < 2) return false;

  const limit = Math.sqrt(num);

  for (let i = 2; i <= limit; i += 1) {
    if (num % i === 0) {
      return false;
    }
  }

  return true;
}
```
