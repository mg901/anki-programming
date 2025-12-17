## [Create a count function](https://bigfrontend.dev/problem/count-function)

```js
function count() {
  count.val = count.val ?? 0;

  return (count.val += 1);
}

count.reset = function () {
  count.val = 0;
};
```
