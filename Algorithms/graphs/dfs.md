## [Depth-first Search 'recursion'](https://www.greatfrontend.com/questions/algo/depth-first-search)

<!-- notecardId: 1749382414756 -->

```js
export default function depthFirstSearch(graph, source) {
  if (!graph || Object.keys(graph).length === 0) return [];

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

<!-- notecardId: 1749382414759 -->

```js
export default function depthFirstSearch(graph, source) {
  if (!graph || Object.keys(graph).length === 0) return [];

  const visited = new Set();
  const stack = [source];
  const result = [];

  while (stack.length) {
    const vertex = stack.pop();
    if (visited.has(vertex)) continue;

    visited.add(vertex);
    result.push(vertex);

    const neighbors = (graph[vertex] ?? []).toReversed();

    for (const neighbor of neighbors) {
      if (visited.has(neighbor)) continue;

      stack.push(neighbor);
    }
  }

  return result;
}
```
