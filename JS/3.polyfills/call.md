## [Function.prototype.call](https://www.greatfrontend.com/questions/javascript/function-call)

```js
Function.prototype.call = function (thisArg, ...args) {
  if (typeof this !== 'function') {
    throw new TypeError(`${this} is not a function`);
  }

  const func = Symbol();
  thisArg = thisArg ?? window;
  thisArg = Object(thisArg);

  thisArg[func] = this;

  const result = thisArg[func](...args);
  delete thisArg[func];

  return result;
};
```
