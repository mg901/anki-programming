## [Fibonacci Number with recursion](https://bigfrontend.dev/problem/Generate-Fibonacci-Number-with-recursion)

<!-- notecardId: 1740217406096 -->

```js
function fib(n, a = 0, b = 1) {
  if (n === 0) return a;
  if (Math.abs(n)) return b;

  // prettier-ignore
  return fib(
    n > 0 ? n - 1 : n + 1, 
    b,
    n > 0 ? a + b : a - b
  );
}
```
