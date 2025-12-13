## [Native Deep Clone](https://learn.javascript.ru/prototype-methods#kratkaya-istoriya)

<!-- notecardId: 1739454879245 -->

```js
Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
);
```
