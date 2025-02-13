## [Write own 'instanceof' operator](https://bigfrontend.dev/problem/write-your-own-instanceof)

<!-- notecardId: 1739476911541 -->

```js
function myInstanceOf(obj, target) {
  if (!target.prototype) {
    throw new TypeError("Right-hand side of 'instanceof' is not an object");
  }

  if (obj == null || typeof obj !== "object") return false;

  let proto = Object.getPrototypeOf(obj);

  while (proto) {
    if (proto === target.prototype) return true;
    proto = Object.getPrototypeOf(proto);
  }

  return false;
}
```
