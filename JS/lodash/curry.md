## [Curry](https://www.greatfrontend.com/questions/javascript/curry?list=lodash)

<!-- notecardId: 1736441773897 -->

```js
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }

    return curried.bind(this, ...args);
  };
}
```
