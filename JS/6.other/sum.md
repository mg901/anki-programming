## [Sum](https://www.greatfrontend.com/questions/javascript/sum?format=javascript)

```js
function sum(a) {
  return (b) => {
    return b === undefined ? a : sum(a + b);
  };
}
```
