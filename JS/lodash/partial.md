## [Partial](https://bigfrontend.dev/problem/implement-partial)

<!-- notecardId: 1739476558939 -->

```js
function partial(func, ...args) {
  return function (...newArgs) {
    return func.apply(this, mergeArgs(args, newArgs));
  };
}

partial.placeholder = Symbol("partial.placeholder");

function mergeArgs(args, newArgs) {
  if (!hasPlaceholder(args)) {
    return [...args, ...newArgs];
  }

  return [
    ...args.map((arg) => (arg === partial.placeholder ? newArgs.shift() : arg)),
    ...newArgs,
  ];
}

function hasPlaceholder(args) {
  return args.includes(partial.placeholder);
}
```
