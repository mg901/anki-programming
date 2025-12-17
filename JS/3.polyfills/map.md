## [Array.prototype.map](https://www.greatfrontend.com/questions/javascript/array-map)

```js
Array.prototype.map = function (callbackFn, thisArg) {
  if (typeof callbackFn !== 'function') {
    throw TypeError(`${callbackFn} is not a function`);
  }

  const n = this.length;
  let result = Array.from(n);

  for (let index = 0; index < n; index += 1) {
    const isNotEmpty = Object.hasOwn(this, index);

    if (isNotEmpty) {
      result[index] = callbackFn.call(thisArg, this[index], index, this);
    }
  }

  return result;
};
```
