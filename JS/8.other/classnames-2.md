## [ClassNames 2](https://www.greatfrontend.com/questions/javascript/classnames-ii?language=js)

```js
function classNames(...args) {
  const classes = new Set();

  collectClasses(args);

  return Array.from(classes).join(' ');

  function collectClasses(...props) {
    for (let i = 0; i < props.length; i += 1) {
      const prop = props[i];

      if (!prop) continue;

      const propType = typeof prop;

      if (propType === 'string' || propType === 'number') {
        classes.add(String(prop));

        continue;
      }

      if (propType === 'function') {
        collectClasses(prop());

        continue;
      }

      if (Array.isArray(prop)) {
        collectClasses(...prop);

        continue;
      }

      if (propType === 'object') {
        for (const key in prop) {
          if (!Object.hasOwn(prop, key)) continue;

          if (prop[key]) {
            classes.add(key);
          } else {
            classes.delete(key);
          }
        }
      }
    }
  }
}
```
