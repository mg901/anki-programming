## [Sum](https://www.greatfrontend.com/questions/javascript/sum?format=javascript)

<!-- notecardId: 1739454886465 -->

```js
function sum(a) {
  return (b) => {
    return b === undefined ? a : sum(a + b);
  };
}
```
