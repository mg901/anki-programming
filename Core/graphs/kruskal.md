## [Kruskal Alrorithm](https://leetcode.com/problems/min-cost-to-connect-all-points/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/f7JOBJIC-NA

// Algorithm: Kruskal
// Explanation:
// - Abdul Bari: https://youtu.be/4ZlRH0eK-qQ?si=zqtaneX9DVkaR3Gx&t=693
class DisjointSet {
  #parent;

  #rank;

  constructor(n) {
    this.#parent = Array.from({ length: n }, (_, index) => index);
    this.#rank = new Uint32Array(n);
  }

  // O(⍺(n))
  find(x) {
    if (this.#parent[x] !== x) {
      this.#parent[x] = this.find(this.#parent[x]);
    }

    return this.#parent[x];
  }

  // O(⍺(n))
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

// Complexity:
// - Time: O(n² log n)
// - Space: O(n²)
function minCostConnectPoints(points) {
  const n = points.length;
  const edges = [];

  for (let u = 0; u < n; u += 1) {
    for (let v = u + 1; v < n; v += 1) {
      const [ux, uy] = points[u];
      const [vx, vy] = points[v];
      const dist = Math.abs(ux - vx) + Math.abs(uy - vy);

      edges.push([u, v, dist]);
    }
  }

  edges.sort((a, b) => a[2] - b[2]);

  const ds = new DisjointSet(n);
  let cost = 0;
  let count = 0;

  for (let [u, v, w] of edges) {
    if (ds.union(u, v)) {
      cost += w;
      count += 1;
      if (count === n - 1) break;
    }
  }

  return cost;
}
```
