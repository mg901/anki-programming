## [Memoize One](https://bigfrontend.dev/problem/implement-memoizeOne)

```js
function memoizeOne(func, isEqual = areArgsEqual) {
  let lastThis;
  let lastArgs;
  let result;

  return function (...newArgs) {
    if (lastThis === this && isEqual(newArgs, lastArgs)) {
      return result;
    }

    result = func.apply(this, newArgs);
    lastThis = this;
    lastArgs = newArgs;

    return result;
  };
}

function areArgsEqual(newArgs, prevArgs) {
  if (newArgs.length !== prevArgs.length) {
    return false;
  }

  for (let i = 0; i < prevArgs.length; i += 1) {
    if (!isStrictEqualWithNaN(newArgs[i], prevArgs[i])) {
      return false;
    }
  }

  return true;
}

function isStrictEqualWithNaN(a, b) {
  if (a === b) return true;

  if (Number.isNaN(a) && Number.isNaN(b)) {
    return true;
  }

  return false;
}
```
