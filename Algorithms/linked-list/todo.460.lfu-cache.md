## [460 LFU Cache](https://leetcode.com/problems/lfu-cache/description/)

```js
class LFUCache {
  #capability;

  #size = 0;

  #minFreq = 1;

  #keyToNode = new Map();

  #keyToFreq = new Map();

  #freqToList = new Map();

  constructor(capacity) {
    this.#capability = capacity;
  }

  get(key) {
    if (!this.#keyToNode.has(key)) return -1;
    this.#updateFreq(key);

    return this.#keyToNode.get(key).getValue().value;
  }

  put(key, value) {
    if (this.#capability === 0) return;

    if (this.#keyToNode.has(key)) {
      const node = this.#keyToNode.get(key);
      node.setValue({ key, value });
      this.#updateFreq(key);

      return;
    }

    if (this.#size === this.#capability) {
      this.#evictLFU();
    }

    const freq = 1;
    const list = this.#freqToList.get(freq) ?? new DoublyLinkedList();
    const node = list.insertFirst({ key, value });

    this.#freqToList.set(freq, list);
    this.#keyToNode.set(key, node);
    this.#keyToFreq.set(key, freq);
    this.#minFreq = 1;
    this.#size += 1;
  }

  #updateFreq(key) {
    const freq = this.#keyToFreq.get(key);
    const node = this.#keyToNode.get(key);
    const list = this.#freqToList.get(freq);

    list.remove(node);

    if (list.isEmpty()) {
      this.#freqToList.delete(freq);
      if (this.#minFreq === freq) this.#minFreq += 1;
    }

    const newFreq = freq + 1;
    const nextList = this.#freqToList.get(newFreq) ?? new DoublyLinkedList();
    const newNode = nextList.insertFirst(node.getValue());

    this.#freqToList.set(newFreq, nextList);
    this.#keyToNode.set(key, newNode);
    this.#keyToFreq.set(key, newFreq);
  }

  #evictLFU() {
    const list = this.#freqToList.get(this.#minFreq);
    const { key } = list.removeLast().getValue();

    this.#keyToNode.delete(key);
    this.#keyToFreq.delete(key);

    if (list.isEmpty()) {
      this.#freqToList.delete(this.#minFreq);
    }

    this.#size -= 1;
  }
}
```
