## async/await

```js
function async(callback) {
  return function (...args) {
    const generator = callback.apply(this, args);

    return execute(generator);
  };
}

function execute(generator, yieldValue) {
  const { done, value } = generator.next(yieldValue);

  if (done) return value;

  return Promise.resolve(value).then(
    (data) => execute(generator, data),
    (reason) => generator.throw(reason),
  );
}
```
