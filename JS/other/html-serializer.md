## [HTML Serializer](https://www.greatfrontend.com/interviews/study/dom-manipulation/questions/javascript/html-serializer)

<!-- notecardId: 1739454859213 -->

```js
function serializeHTML(element, indent = "\t") {
  const NEW_LINE = "\n";

  return traverse(element);

  function traverse(item, depth = 0) {
    if (typeof item === "string") {
      return `${indent.repeat(depth)}${item}`;
    }

    return [
      `${indent.repeat(depth)}<${item.tag.toLowerCase()}>`,
      item.children
        .flatMap((child) => traverse(child, depth + 1))
        .join(NEW_LINE),
      `${indent.repeat(depth)}</${item.tag.toLowerCase()}>`,
    ].join(NEW_LINE);
  }
}
```
