## [Promisify 2](https://www.greatfrontend.com/questions/javascript/promisify-ii)

```js
const symbol = Symbol.for('util.promisify.custom');

function promisify(func) {
  if (Object.hasOwn(func, symbol)) {
    return func[symbol];
  }

  return function (...args) {
    return new Promise((resolve, reject) => {
      func.call(this, ...args, (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data);
        }
      });
    });
  };
}
```
