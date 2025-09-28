## [2648 Generate Fibonacci Sequence](https://leetcode.com/problems/generate-fibonacci-sequence/description/)

```js
// - Time: O(n)
// - Space: O(1)
function* fibGenerator() {
  let a = 0;
  let b = 1;

  while (true) {
    yield a;

    const temp = a;
    a = b;
    b = temp + b;
  }
}
```
