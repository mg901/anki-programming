## [Jest spyOn](https://bigfrontend.dev/problem/implement-spyOn)

<!-- notecardId: 1739454867582 -->

```js
// HOF
function spyOn(o, methodName) {
  const calls = [];

  if (!Object.hasOwn(o, methodName) && typeof o[methodName] !== "function") {
    throw new Error("");
  }

  const originalMethod = o[methodName];

  o[methodName] = function (...args) {
    calls.push(args);
    originalMethod.apply(o, args);
  };

  return { calls };
}

// Proxy
function spyOn(o, methodName) {
  const calls = [];

  if (!Object.hasOwn(o, methodName) && typeof o[methodName] !== "function") {
    throw new Error("");
  }

  const proxy = new Proxy(o[methodName], {
    apply(target, thisArg, args) {
      calls.push(args);

      target.apply(thisArg, args);
    },
  });

  o[methodName] = proxy;

  return { calls };
}
```
