## [Disjoint-Set](https://legendary-zebra-xj456pwj726w95.github.dev/)

<!-- notecardId: 1756393142878 -->

```js
class DisjointSet {
  #parent;

  #rank;

  constructor(n) {
    this.#parent = Array.from({ length: n }, (_, index) => index);
    this.#rank = new Uint32Array(n);
  }

  find(x) {
    if (this.#parent[x] !== x) {
      this.#parent[x] = this.find(this.#parent[x]);
    }

    return this.#parent[x];
  }

  union(x, y) {
    const rootX = this.find(x);
    const rootY = this.find(y);

    if (rootX === rootY) return false;

    if (this.#rank[rootX] < this.#rank[rootY]) {
      this.#parent[rootX] = rootY;
    } else if (this.#rank[rootX] > this.#rank[rootY]) {
      this.#parent[rootY] = rootX;
    } else {
      this.#parent[rootY] = rootX;
      this.#rank[rootX] += 1;
    }

    return true;
  }
}
```
