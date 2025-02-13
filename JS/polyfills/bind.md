## [Function.prototype.bind](https://www.greatfrontend.com/questions/javascript/function-bind)

<!-- notecardId: 1739475831263 -->

```js
Function.prototype.bind = function (context, ...args) {
  if (typeof this !== "function") {
    throw new TypeError("Bind must be called on a function");
  }

  const func = this;

  function boundFunction(...boundArgs) {
    if (this instanceof boundFunction) {
      return new func([...boundArgs, ...args]);
    }

    return func.apply(context, [...boundArgs, ...args]);
  }

  if (func.prototype) {
    boundFunction.prototype = Object.create(func.prototype);
  }

  return boundFunction;
};

// Example
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const BoundPerson = Person.bind(null, "John");

const person = new BoundPerson(30);
console.log(person.name); // "John"
console.log(person.age); // 30
console.log(person instanceof Person); // true
```
