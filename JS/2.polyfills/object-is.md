## [Object.is](https://bigfrontend.dev/problem/implement-Object.is)

<!-- notecardId: 1739475860523 -->

```js
function is(a, b) {
  if (a !== a && b !== b) {
    return true;
  }

  if (a === 0 && b === 0) {
    return 1 / a === 1 / b; // false
  }

  return a === b;
}
```
