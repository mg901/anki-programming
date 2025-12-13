## [Memoize 2](https://www.greatfrontend.com/questions/javascript/memoize-ii)

<!-- notecardId: 1765667575758 -->

```js
export default function memoize(func) {
  const cache = new Trie();

  return function (...args) {
    const node = cache.get(args);

    if (node.hasValue) return node.value;

    const result = func.apply(this, args);
    cache.set(args, result);

    return result;
  };
}

class TrieNode {
  value = undefined;

  hasValue = false;

  children = new Map();
}

class Trie {
  #root = new TrieNode();

  get(args) {
    let node = this.#root;

    for (const arg of args) {
      if (!node.children.has(arg)) {
        return new TrieNode();
      }

      node = node.children.get(arg);
    }

    return node;
  }

  set(args, value) {
    let node = this.#root;

    for (const arg of args) {
      if (!node.children.has(arg)) {
        node.children.set(arg, new TrieNode());
      }

      node = node.children.get(arg);
    }

    node.value = value;
    node.hasValue = true;
  }
}
```
