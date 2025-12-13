## [Create "new" operator](https://bigfrontend.dev/problem/create-your-own-new-operator)

<!-- notecardId: 1739476915793 -->

```js
function myNew(constructor, ...args) {
  const instance = Object.create(constructor.prototype);
  const result = constructor.apply(instance, args);

  return result ?? instance;
}
```
