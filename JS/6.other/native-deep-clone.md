## [Native Deep Clone](https://learn.javascript.ru/prototype-methods#kratkaya-istoriya)

```js
Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj),
);
```
