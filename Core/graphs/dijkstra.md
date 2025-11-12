## Dijkstra

```js
import { MinPriorityQueue } from '@datastructures-js/priority-queue';

function dijkstra(n, edges, start) {
  const graph = createGraph(n + 1, edges);
  const dist = new Array(n + 1).fill(Infinity);
  dist[start] = 0;

  const minpq = new MinPriorityQueue(([, w]) => w);
  minpq.enqueue([start, 0]);

  while (!minpq.isEmpty()) {
    const [u, distance] = minpq.dequeue();
    if (distance > dist[u]) continue;

    for (const [v, w] of graph[u]) {
      if (dist[u] + w < dist[v]) {
        dist[v] = dist[u] + w;

        minpq.enqueue([v, dist[v]]);
      }
    }
  }

  return dist;
}

function createGraph(n, edges) {
  const graph = Array.from({ length: n }, () => []);

  for (const [u, v, w] of edges) {
    graph[u].push([v, w]);
  }

  return graph;
}
```
