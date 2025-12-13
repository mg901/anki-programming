## [Curry with placeholder](https://bigfrontend.dev/problem/implement-curry-with-placeholder)

<!-- notecardId: 1739476479292 -->

```js
function curry(fn) {
  return function curried(...args) {
    if (!hasPlaceholder(args) && args.length >= fn.length) {
      return fn.apply(this, args);
    }

    return function (...newArgs) {
      return curried.apply(this, mergeArgs(args, newArgs));
    };
  };
}

curry.placeholder = Symbol("curry.placeholder");

function mergeArgs(args, newArgs) {
  if (!hasPlaceholder(args)) {
    return [...args, ...newArgs];
  }

  return [
    ...args.map((arg) => (arg === curry.placeholder ? newArgs.shift() : arg)),
    ...newArgs,
  ];
}

function hasPlaceholder(args) {
  return args.includes(curry.placeholder);
}
```
