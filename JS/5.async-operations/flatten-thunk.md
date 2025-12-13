## [Flatten Thunk 'promises'](https://bigfrontend.dev/problem/flatten-Thunk)

<!-- notecardId: 1739475038556 -->

```js
function flattenThunk(thunk) {
  return function (callback) {
    return promisify(thunk).then(
      (value) => {
        callback(null, value);
      },
      (reason) => {
        callback(reason);
      }
    );
  };
}

function promisify(func) {
  return new Promise((resolve, reject) => {
    func((error, data) => {
      if (error) {
        reject(error);

        return;
      }

      if (typeof data !== "function") {
        resolve(data);

        return;
      }

      resolve(promisify(data));
    });
  });
}
```

## [Flatten Thunk 'callbacks'](https://bigfrontend.dev/problem/flatten-Thunk)

<!-- notecardId: 1739475038558 -->

```js
function flattenThunk(thunk) {
  return function (callback) {
    thunk((error, data) => {
      if (error) {
        callback(error);

        return;
      }

      if (typeof data !== "function") {
        callback(null, data);

        return;
      }

      flattenThunk(data)(callback);
    });
  };
}
```
