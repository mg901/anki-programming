## [Create a sum](https://bigfrontend.dev/problem/create-a-sum)

```js
function sum(a) {
  const wrapper = (b) => sum(a + b);

  wrapper[Symbol.toPrimitive] = () => a;

  return wrapper;
}
```
