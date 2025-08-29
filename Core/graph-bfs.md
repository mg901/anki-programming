## [Graph BFS](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393149390 -->

```js
function bfs(graph, source) {
  if (!graph || Object.keys(graph).length === 0) return [];

  const visited = new Set();
  const queue = [source];
  const result = [];

  while (queue.length) {
    const u = queue.shift();
    if (visited.has(u)) continue;

    visited.add(u);
    result.push(u);

    for (const v of graph[u] ?? []) {
      if (!visited.has(v)) {
        queue.push(v);
      }
    }
  }

  return result;
}
```
