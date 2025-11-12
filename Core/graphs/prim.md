## [Prim Algorithm](https://leetcode.com/problems/min-cost-to-connect-all-points/description/)

```js
// Explanation:
// - Neetcode: https://youtu.be/f7JOBJIC-NA

// Algorithm: Prim
// Explanation:
// - Abdul Bari: https://youtu.be/4ZlRH0eK-qQ?si=HtVs9yDNVg6DIRNC&t=466

// Complexity:
// - Time: O(n²)
// - Space: O(n)
function minCostConnectPoints(points) {
  const n = points.length;
  const visited = new Uint8Array(n);
  const key = Array(n).fill(Infinity);
  key[0] = 0;

  let cost = 0;

  for (let i = 0; i < n; i += 1) {
    let u = -1; // virtual starting point

    for (let v = 0; v < n; v += 1) {
      if (visited[v]) continue;
      if (u === -1 || key[v] < key[u]) {
        u = v;
      }
    }

    visited[u] = 1;
    cost += key[u];

    const [ux, uy] = points[u];
    for (let v = 0; v < n; v += 1) {
      if (visited[v]) continue;

      const [vx, vy] = points[v];
      const dist = Math.abs(ux - vx) + Math.abs(uy - vy);
      key[v] = Math.min(key[v], dist);
    }
  }

  return cost;
}

// Or
function minCostConnectPoints(points) {
  const n = points.length;
  const key = new Array(n).fill(Infinity);
  const visited = new Uint8Array(n);

  let u = 0;
  let nodesConnected = 0;
  let cost = 0;

  while (nodesConnected < n - 1) {
    visited[u] = 1;
    let nextU = -1;

    for (let v = 0; v < n; v += 1) {
      if (visited[v]) continue;

      const [ux, uy] = points[u];
      const [vx, vy] = points[v];
      const dist = Math.abs(ux - vx) + Math.abs(uy - vy);
      key[v] = Math.min(key[v], dist);

      if (nextU === -1 || key[v] < key[nextU]) {
        nextU = v;
      }
    }

    cost += key[nextU];
    u = nextU;
    nodesConnected += 1;
  }

  return cost;
}
```
