## [Array.prototype.filter](https://www.greatfrontend.com/questions/javascript/array-filter)

<!-- notecardId: 1739475843344 -->

```js
Array.prototype.filter = function (callbackFn, thisArg) {
  if (typeof callbackFn !== "function") {
    throw new TypeError(`${callbackFn} is not a function`);
  }

  let result = [];

  for (let index = 0; index < this.length; index += 1) {
    const item = this[index];

    if (callbackFn.call(thisArg, item, index, this)) {
      result[index] = item;
    }
  }

  return result;
};
```
