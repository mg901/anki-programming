## [Memoize 2](https://www.greatfrontend.com/questions/javascript/memoize-ii)

<!-- notecardId: 1765726956290 -->

```js
class TrieNode {
  children = new Map();

  hasValue = false;

  value = undefined;
}

class Cache {
  #root = new TrieNode();

  set(args, value) {
    let node = this.#root;

    for (const char of args) {
      if (!node.children.has(char)) {
        node.children.set(char, new TrieNode());
      }

      node = node.children.get(char);
    }

    node.hasValue = true;
    node.value = value;
  }

  get(args) {
    let node = this.#root;

    for (const char of args) {
      node = node.children.get(char) ?? new TrieNode();
    }

    return node;
  }
}

export default function memoize(func) {
  const cache = new Cache();

  return function (...args) {
    const node = cache.get(args);
    if (node.hasValue) return node.value;

    const value = func.apply(this, args);
    cache.set(args, value);

    return value;
  };
}
```
