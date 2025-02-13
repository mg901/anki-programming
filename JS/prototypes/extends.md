## [Custom Extends](https://bigfrontend.dev/problem/write-your-own-extends-in-es5)

<!-- notecardId: 1739476908125 -->

```js
// Modern
const myExtends = (Parent, Child) => {
  function Extended(...args) {
    Parent.apply(this, args);
    Child.apply(this, args);

    Object.setPrototypeOf(this, Child.prototype);
  }

  Object.setPrototypeOf(Child.prototype, Parent.prototype);
  Object.setPrototypeOf(Extended, Parent);

  return Extended;
};

// Old-school
const myExtends = (Parent, Child) => {
  function Extended(...args) {
    Parent.apply(this, args);
    Child.apply(this, args);

    this.__proto__ = Child.prototype;
  }

  Child.prototype.__proto__ = Parent.prototype;
  Extended.__proto__ = Parent;

  return Extended;
};
```
