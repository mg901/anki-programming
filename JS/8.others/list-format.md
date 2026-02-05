## [List Format](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/list-format)

```js
function listFormat(items, options = {}) {
  let array = items.filter(Boolean);

  if (array.length === 0) return '';
  if (array.length === 1) return items.at(0);

  const { sorted, unique, length } = options;

  if (sorted) {
    array.sort();
  }

  if (unique) {
    array = Array.from(new Set(array));
  }

  let suffix;
  let limit;

  if (length && length > 0 && length < array.length) {
    const diff = array.length - length;

    limit = length;
    suffix = `${diff} other${diff > 1 ? 's' : ''}`;
  } else {
    limit = -1;
    suffix = array.at(-1);
  }

  return `${array.slice(0, limit).join(', ')} and ${suffix}`;
}
```
