## [Topological Sort 'Adjacent List'](https://www.greatfrontend.com/questions/algo/topological-sort)

```js
// Explanation:
// - Algorithm: Kahn
// - Neetcode: https://youtu.be/7J3GadLzydI?si=0xVzE1Iot1swC792

// Complexity:
// - Time: O(V + E)
// - Space: O(V + Е)
export default function topologicalSort(graph) {
  const nodes = Object.keys(graph);
  const nodeMetadataMap = new Map();
  const queue = [];
  const result = [];

  for (const node of nodes) {
    nodeMetadataMap.set(node, {
      in: 0,
      out: new Set(graph[node]),
    });
  }

  for (const u of nodes) {
    for (const v of graph[u] ?? []) {
      nodeMetadataMap.get(v).in += 1;
    }
  }

  for (const [u, metadata] of nodeMetadataMap) {
    if (metadata.in === 0) {
      queue.push(u);
    }
  }

  while (queue.length) {
    const u = queue.shift();
    result.push(u);

    for (const v of graph[u] ?? []) {
      nodeMetadataMap.get(v).in -= 1;

      if (nodeMetadataMap.get(v).in === 0) {
        queue.push(v);
      }
    }
  }

  return result.length === nodes.length ? result : [];
}
```
