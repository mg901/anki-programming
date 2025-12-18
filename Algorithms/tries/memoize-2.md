## [Memoize 2](https://www.greatfrontend.com/questions/javascript/memoize-ii)

```js
class TrieNode {
  #children = new Map();

  #hasValue = false;

  #value;

  get hasValue() {
    return this.#hasValue;
  }

  set value(value) {
    this.#value = value;
    this.#hasValue = true;
  }

  get value() {
    return this.#value;
  }

  getChild(key) {
    return this.#children.get(key);
  }

  ensureChild(key) {
    let child = this.#children.get(key);

    if (!child) {
      child = new TrieNode();
      this.#children.set(key, child);
    }

    return child;
  }
}

class TrieCache {
  #root = new TrieNode();

  getNode(args) {
    let node = this.#root;

    for (const arg of args) {
      node = node.getChild(arg);

      if (!node) return null;
    }

    return node;
  }

  set(args, value) {
    let node = this.#root;

    for (const arg of args) {
      node = node.ensureChild(arg);
    }

    node.value = value;
  }
}

export default function memoize(func) {
  const cache = new TrieCache();

  return function (...args) {
    const node = cache.getNode(args);
    if (node?.hasValue) return node.value;

    const value = func.apply(this, args);
    cache.set(args, value);

    return value;
  };
}
```
