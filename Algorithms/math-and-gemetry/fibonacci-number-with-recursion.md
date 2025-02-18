## [Fibonacci Number with recursion](https://bigfrontend.dev/problem/Generate-Fibonacci-Number-with-recursion)

<!-- notecardId: 1739828523289 -->

```js
function fib(n, a = 1, b = 1) {
  if (n === 0) return 0;
  if (n <= 2) return b;

  return fib(n - 1, b, a + b);
}
```
