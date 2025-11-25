## [211 Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

```js
class TrieNode {
  children = new Map();

  isEndOfWord = false;
}

class WordDictionary {
  root = new TrieNode();

  addWord(word) {
    let node = this.root;

    for (const char of word) {
      if (!node.children.has(char)) {
        node.children.set(char, new TrieNode());
      }

      node = node.children.get(char);
    }

    node.isEndOfWord = true;
  }

  search(word) {
    return this.#dfs(0, word, this.root);
  }

  #dfs(index, word, node) {
    if (index === word.length) {
      return node.isEndOfWord;
    }

    const char = word[index];

    if (char === '.') {
      for (const child of node.children.values()) {
        if (this.#dfs(index + 1, word, child)) return true;
      }

      return false;
    }

    if (!node.children.has(char)) return false;

    return this.#dfs(index + 1, word, node.children.get(char));
  }
}
```
