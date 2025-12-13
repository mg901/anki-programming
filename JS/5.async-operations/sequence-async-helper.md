## [Sequence async helper 'promises'](https://bigfrontend.dev/problem/implement-async-helper-sequence)

<!-- notecardId: 1739475088361 -->

```js
function sequence(funcs) {
  return (callback, start) => {
    funcs
      .map(promisify)
      .reduce((acc, fn) => acc.then(fn), Promise.resolve(start))
      .then((data) => {
        callback(null, data);
      })
      .catch(callback);
  };
}

function promisify(func) {
  return (value) => {
    return new Promise((resolve, reject) => {
      func((error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data);
        }
      }, value);
    });
  };
}
```

## [Sequence async helper 'callbacks'](https://bigfrontend.dev/problem/implement-async-helper-sequence)

<!-- notecardId: 1739475088365 -->

```js
function sequence(funcs) {
  return function (callback, start) {
    let index = 0;

    next(null, start);

    function next(error, data) {
      if (error) {
        callback(error);

        return
      }

      if (index === funcs.length) {
        callback(null, data);

        return
      }

      const fn = funcs[index];
      index += 1;
      fn(next, data);
    }
  };
```
