## Problem 1

<!-- notecardId: 1739476920118 -->

```js
/*
Вопросы:
  1) Что выведет код?
  2) Почему так происходит?

*/
function A() {
  this.value = 42;
}

A.prototype.getValue = function () {
  return this.value;
};

function B() {
  this.value = 100;
}

B.prototype = new A();

const a = new A();
const b = new B();

console.log(b.getValue());
delete b.value;
console.log(b.getValue());
```

## Problem 2

<!-- notecardId: 1739476920123 -->

```js
/*
Вопросы:
  1) Что выведет код?
  2) Почему delete ведёт себя так?
*/
function A() {}

A.prototype.x = 10;

const a = new A();
const b = Object.create(a);

b.x = 20;

delete b.x;

console.log(b.x);
delete A.prototype.x;
console.log(b.x);
```

## Problem 3

<!-- notecardId: 1739476920126 -->

```js
/*
Вопросы:
  1) Что выведет код?
  2) Почему второе изменение A.prototype не повлияло на a?
*/
function A() {}

A.prototype = {
  x: 10,
  getX() {
    return this.x;
  },
};

const a = new A();

A.prototype.x = 20;
console.log(a.getX());

A.prototype = {
  x: 30,
  getX() {
    return this.x;
  },
};
console.log(a.getX());
```

## Problem 4

<!-- notecardId: 1739476920129 -->

```js
/*
Вопросы:
  1) Что выведет код?
  2) Почему a undefined?
  3) Что хранится в globalThis.value?
*/
function A() {
  this.value = 42;
}

A.prototype.getValue = function () {
  return this.value;
};

const a = A();
console.log(a);
console.log(globalThis.value || window.value);
```

## Problem 5

<!-- notecardId: 1739476920132 -->

```js
/*
Вопросы:
  1) Почему Child.prototype = Object.create(Parent.prototype) важен?
  2) Что произойдёт, если убрать Child.prototype.constructor = Child?
  3) Почему child instanceof Parent даёт true, хотя Parent явно не создавал этот объект?
 */

function Parent(name) {
  this.name = name;
}

Parent.prototype.sayHello = function () {
  return `Hello, ${this.name}`;
};

function Child(name, age) {
  Parent.call(this, name);
  this.age = age;
}

Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;

Child.prototype.getAge = function () {
  return this.age;
};

const child = new Child("Max", 30);
console.log(child.sayHello());
console.log(child.getAge());
console.log(child instanceof Parent);
console.log(child instanceof Child);
```
