## [Depth-first Search 'recursion'](https://www.greatfrontend.com/questions/algo/depth-first-search)

<!-- notecardId: 1765740875941 -->

```js
// Explanation:
// - William Ficet: https://youtu.be/7fujbpJ0LB4?si=cQimqTmpQr0frQxz
// - FreeCodeCamp.org: https://youtu.be/tWVWeAqZ0WU?si=TcA9Wwxi1cINeDRt&t=604

// Complexity:
// - Time: O(v + e)
//   where:
//    v = vertexes
//    e = edges
// - Space: O(v)
export default function depthFirstSearch(graph, source) {
  if (!graph || !Object.keys(graph).length) return [];

  const visited = new Set();
  const result = [];
  traverse(source);

  return result;

  function traverse(u) {
    if (visited.has(u)) return;

    visited.add(u);
    result.push(u);

    for (const v of graph[u] ?? []) {
      traverse(v);
    }
  }
}
```

## [Depth-first Search 'imperative'](https://www.greatfrontend.com/questions/algo/depth-first-search)

<!-- notecardId: 1765740875944 -->

```js
// Complexity:
// - Time: O(v + e)
//   where:
//    v = vertexes
//    e = edges
// - Space: O(v)
export default function depthFirstSearch(graph, source) {
  if (!graph || !Object.keys(graph).length) return [];

  const result = [];
  const stack = [source];
  const visited = new Set();

  while (stack.length) {
    const u = stack.pop();
    if (visited.has(u)) continue;

    result.push(u);
    visited.add(u);

    const neighbors = graph[u] ?? [];
    const n = neighbors.length;

    for (let i = n - 1; i >= 0; i -= 1) {
      const neighbor = neighbors[i];

      if (!visited.has(neighbor)) {
        stack.push(neighbor);
      }
    }
  }

  return result;
}
```
