## [Breadth-first Search](https://www.greatfrontend.com/questions/algo/breadth-first-search?format=algo)

<!-- notecardId: 1750164122565 -->

```js
export default function breadthFirstSearch(graph, source) {
  if (!graph || Object.keys(graph).length === 0) return [];

  const visited = new Set();
  const queue = [source];
  const result = [];

  while (queue.length) {
    const vertex = queue.shift();

    if (visited.has(vertex)) continue;
    visited.add(vertex);
    result.push(vertex);

    const neighbors = graph[vertex] ?? [];

    for (const neighbor of neighbors) {
      if (visited.has(neighbor)) continue;
      queue.push(neighbor);
    }
  }

  return result;
}
```
