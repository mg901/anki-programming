## [Memoize 2](https://www.greatfrontend.com/questions/javascript/memoize-ii)

<!-- notecardId: 1766334522236 -->

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

  get(args) {
    let node = this.#root;
    const NOT_FOUND = [false, null];

    for (const arg of args) {
      const child = node.getChild(arg);
      if (!child) return NOT_FOUND;

      node = child;
    }

    return node.hasValue ? [true, node.value] : NOT_FOUND;
  }

  set(args, value) {
    let node = this.#root;

    for (const arg of args) {
      node = node.ensureChild(arg);
    }

    node.value = value;
  }

  clear() {
    this.#root = new TrieNode();
  }
}

export default function memoize(func) {
  const cache = new TrieCache();

  return function (...args) {
    const [found, value] = cache.get(args);
    if (found) return value;

    const result = func.apply(this, args);
    cache.set(args, result);

    return result;
  };
}
```
