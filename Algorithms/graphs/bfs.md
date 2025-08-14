## [Breadth-first Search](https://www.greatfrontend.com/questions/algo/breadth-first-search?format=algo)

<!-- notecardId: 1755202212359 -->

```js
// Explanation:
// - William Ficet: https://youtu.be/oDqjPvD54Ss?si=nh4oHyJ-noSLn5v0
// - FreeCodeCamp.org: https://youtu.be/tWVWeAqZ0WU?si=e5P5Pku60aEYwQyn&t=648

// Complexity:
// - Time: O(v + e)
//   where:
//    v = vertexes
//    e = edges
// - Space: O(v)
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
