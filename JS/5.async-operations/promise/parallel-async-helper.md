## [Parallel async helper 'promises'](https://bigfrontend.dev/problem/implement-async-helper-parallel)

```js
function parallel(funcs) {
  return (callback) => {
    Promise.all(funcs.map(promisify))
      .then((values) => {
        callback(null, values);
      })
      .catch(callback);
  };
}

function promisify(func) {
  return new Promise((resolve, reject) => {
    func((error, data) => {
      if (error) {
        reject(error);
      } else {
        resolve(data);
      }
    });
  });
}
```

## [Parallel async helper 'callbacks'](https://bigfrontend.dev/problem/implement-async-helper-parallel)

```js
function parallel(funcs) {
  return (callback) => {
    const results = [];
    let hasError = false;

    if (!funcs.length) {
      callback(null, results);

      return;
    }

    funcs.forEach((func, index) => {
      func((error, data) => {
        if (hasError) return;

        if (error) {
          hasError = true;
          callback(error);

          return;
        }

        results[index] = data;

        if (results.length === funcs.length) {
          callback(null, results);
        }
      });
    });
  };
}
```
