## [Promise.race](https://www.greatfrontend.com/questions/javascript/promise-race)

<!-- notecardId: 1739475500250 -->

```js
function promiseRace(iterable) {
  return new Promise((resolve, reject) => {
    for (const promise of iterable) {
      Promise.resolve(promise).then(resolve, reject);
    }
  });
}
```
