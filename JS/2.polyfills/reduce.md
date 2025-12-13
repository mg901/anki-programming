## [Array.prototype.reduce](https://bigfrontend.dev/problem/implement-Array-prototype-reduce)

<!-- notecardId: 1739475864628 -->

```js
Array.prototype.myReduce = function (...args) {
  let callback = args[0];
  let defaultValue = args[1];
  let thisArg = args[2];
  const noDefaultValue = args.length < 2;

  if (typeof callback !== 'function') {
    throw new TypeError(`${typeof callback} is not a function`);
  }

  const n = this.length;

  if (n === 0 && noDefaultValue) {
    throw new TypeError('Reduce of empty array with no initial value');
  }

  let acc = noDefaultValue ? this.at(0) : defaultValue;
  let initialIndex = noDefaultValue ? 1 : 0;

  for (let i = initialIndex; i < n; i += 1) {
    if (Object.hasOwn(this, i)) {
      acc = callback.call(thisArg, acc, this[i], i, this);
    }
  }

  return acc;
};
```
