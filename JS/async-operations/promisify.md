## [Promisify](https://www.greatfrontend.com/questions/javascript/promisify)

<!-- notecardId: 1739475068860 -->

```js
function promisify(func) {
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
