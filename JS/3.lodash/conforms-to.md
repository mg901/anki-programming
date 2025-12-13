## [conformsTo](https://www.greatfrontend.com/questions/javascript/conforms-to?language=js)

<!-- notecardId: 1739476474989 -->

```js
function conformsTo(o, source) {
  for (const key in source) {
    if (!Object.hasOwn(source, key)) continue;

    if (!Object.hasOwn(o, key) || !source[key](o[key])) {
      return false;
    }
  }

  return true;
}
```
