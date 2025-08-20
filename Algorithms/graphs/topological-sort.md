## [Topological Sort 'Kahn'](https://www.greatfrontend.com/questions/algo/topological-sort)

<!-- notecardId: 1755631076514 -->

```js
// Explanation:
// - Algorithm: Kahn
// - Neetcode: https://youtu.be/7J3GadLzydI?si=0xVzE1Iot1swC792

// Complexity:
// - Time: O(V + E)
// - Space: O(V)
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

  for (const node of nodes) {
    for (const neighbor of graph[node]) {
      nodeMetadataMap.get(neighbor).in += 1;
    }
  }

  for (const [node, metadata] of nodeMetadataMap) {
    if (metadata.in === 0) {
      queue.push(node);
    }
  }

  while (queue.length) {
    const node = queue.shift();
    result.push(node);

    for (const neighbor of nodeMetadataMap.get(node).out) {
      nodeMetadataMap.get(neighbor).in -= 1;

      if (nodeMetadataMap.get(neighbor).in === 0) {
        queue.push(neighbor);
      }
    }
  }

  return result.length === nodes.length ? result : [];
}
```
