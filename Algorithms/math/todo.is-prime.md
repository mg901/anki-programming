## [Is Prime](https://bigfrontend.dev/problem/isPrime)

```js
// - Time: O()
// - Space: O(1)
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
