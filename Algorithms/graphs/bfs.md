## [Breadth-first Search](https://www.greatfrontend.com/questions/algo/breadth-first-search?format=algo)

<!-- notecardId: 1749314138495 -->

```js
export default function breadthFirstSearch(graph, source) {
  if (!graph || Object.keys(graph).length === 0) return [];

  const visited = new Set();
  const queue = new Queue();
  queue.enqueue(source);

  const result = [];

  while (queue.length) {
    const vertex = queue.dequeue();

    if (visited.has(vertex)) continue;
    visited.add(vertex);
    result.push(vertex);

    const neighbors = graph[vertex] ?? [];

    for (const neighbor of neighbors) {
      if (visited.has(neighbor)) continue;
      queue.enqueue(neighbor);
    }
  }

  return result;
}
```
