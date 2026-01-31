## [Curry 3](https://www.greatfrontend.com/questions/javascript/curry-iii?format=javascript)

```js
function curry(func) {
  return function curried(...args) {
    const bound = curried.bind(this, ...args);

    bound[Symbol.toPrimitive] = () => func.apply(this, args);

    return bound;
  };
}
```
