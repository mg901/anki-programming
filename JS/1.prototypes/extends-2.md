## [Custom Extends 2](https://www.notion.so/mg901/Second-Brain-d073ffed28ee45e8955bfb73a5d40389?p=682e6f69d7ec4b52bd99583f1bde8716&pm=s)

<!-- notecardId: 1739476904113 -->

```js
function _extend(Parent, Child) {
  Object.defineProperties(Child.prototype, {
    _super: {
      value: Parent,
    },
  });

  Object.setPrototypeOf(Child.prototype, Parent.prototype);
  Object.setPrototypeOf(Child, Parent);

  return Child;
}
```
