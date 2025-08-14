## [Depth-first Search 'recursion'](https://www.greatfrontend.com/questions/algo/depth-first-search)

<!-- notecardId: 1755202200586 -->

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
  if (graph == null || Object.keys(graph).length === 0) return [];

  const visited = new Set();
  const result = [];
  traverse(source);

  return result;

  function traverse(vertex) {
    if (visited.has(vertex)) return;

    visited.add(vertex);
    result.push(vertex);

    const neighbors = graph[vertex] ?? [];

    for (const neighbor of neighbors) {
      traverse(neighbor);
    }
  }
}
```

## [Depth-first Search 'imperative'](https://www.greatfrontend.com/questions/algo/depth-first-search)

<!-- notecardId: 1755202200588 -->

```js
// Complexity:
// - Time: O(v + e)
//   where:
//    v = vertexes
//    e = edges
// - Space: O(v)
export default function depthFirstSearch(graph, source) {
  if (graph == null || Object.keys(graph).length === 0) return [];

  const result = [];
  const stack = [source];
  const visited = new Set();

  while (stack.length) {
    const vertex = stack.pop();
    if (visited.has(vertex)) continue;

    result.push(vertex);
    visited.add(vertex);

    const neighbors = graph[vertex] ?? [];

    for (let i = neighbors.length - 1; i >= 0; i -= 1) {
      const neighbor = neighbors[i];

      if (!visited.has(neighbor)) {
        stack.push(neighbor);
      }
    }
  }

  return result;
}
```
