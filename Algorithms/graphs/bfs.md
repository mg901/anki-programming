## [Breadth-first Search](https://www.greatfrontend.com/questions/algo/breadth-first-search?format=algo)

<!-- notecardId: 1765740721670 -->

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
  if (!graph || !Object.keys(graph).length) return [];

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
