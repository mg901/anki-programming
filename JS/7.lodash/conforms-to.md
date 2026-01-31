## [conformsTo](https://www.greatfrontend.com/questions/javascript/conforms-to?language=js)

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
