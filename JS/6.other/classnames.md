## [Classnames](https://www.greatfrontend.com/questions/javascript/classnames?language=js)

```js
function classNames(...args) {
  const classes = [];

  for (let i = 0; i < args.length; i += 1) {
    const arg = args[i];

    if (!arg) continue;

    const type = typeof arg;

    if (type === 'string' || type === 'number') {
      classes.push(arg);
      continue;
    }

    if (Array.isArray(arg)) {
      if (arg.length) {
        const result = classNames(...arg);

        if (result.length) {
          classes.push(result);
        }
      }
      continue;
    }

    if (type === 'object') {
      if (arg.toString === Object.prototype.toString) {
        for (const key in arg) {
          if (!Object.hasOwn(arg, key)) continue;

          if (arg[key]) {
            classes.push(key);
          }
        }
      } else {
        classes.push(arg.toString());
      }
    }
  }

  return classes.join(' ');
}
```
