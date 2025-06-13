## [Topological Sort 'Kahn's algorithm'](https://www.greatfrontend.com/questions/algo/topological-sort)

<!-- notecardId: 1749814240574 -->

```js
export default function topologicalSort(graph) {
  const nodes = new Map();
  const queue = new Queue();
  const order = [];
  const graphNodes = Object.keys(graph);

  graphNodes.forEach((node) => {
    nodes.set(node, {
      in: 0,
      out: new Set(graph[node]),
    });
  });

  graphNodes.forEach((node) => {
    graph[node].forEach((neighbor) => {
      nodes.get(neighbor).in += 1;
    });
  });

  nodes.forEach((value, node) => {
    if (value.in === 0) {
      queue.enqueue(node);
    }
  });

  while (queue.length()) {
    const node = queue.dequeue();

    nodes.get(node).out.forEach((neighbor) => {
      nodes.get(neighbor).in -= 1;

      if (nodes.get(neighbor).in === 0) {
        queue.enqueue(neighbor);
      }
    });

    order.push(node);
  }

  return order.length === graphNodes.length ? order : [];
}

// or
export default function topologicalSort(graph) {
  const nodes = new Map();
  const queue = [];
  const order = [];
  const graphNodes = Object.keys(graph);

  for (const node of graphNodes) {
    nodes.set(node, {
      in: 0,
      out: new Set(graph[node]),
    });
  }

  for (const node of graphNodes) {
    for (const neighbor of graph[node]) {
      nodes.get(neighbor).in += 1;
    }
  }

  for (const [node, value] of nodes) {
    if (value.in === 0) {
      queue.push(node);
    }
  }

  while (queue.length) {
    const node = queue.shift();

    for (const neighbor of nodes.get(node).out) {
      nodes.get(neighbor).in -= 1;

      if (nodes.get(neighbor).in === 0) {
        queue.push(neighbor);
      }
    }

    order.push(node);
  }

  return order.length === graphNodes.length ? order : [];
}
```
