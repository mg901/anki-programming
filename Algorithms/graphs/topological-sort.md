## [Topological Sort 'Kahn's algorithm'](https://www.greatfrontend.com/questions/algo/topological-sort)

<!-- notecardId: 1749839117079 -->

```js
export default function topologicalSort(graph) {
  const nodeMetadata = new Map();
  const queue = new Queue();
  const order = [];
  const graphNodes = Object.keys(graph);

  graphNodes.forEach((node) => {
    nodeMetadata.set(node, {
      in: 0,
      out: new Set(graph[node]),
    });
  });

  graphNodes.forEach((node) => {
    graph[node].forEach((neighbor) => {
      nodeMetadata.get(neighbor).in += 1;
    });
  });

  nodeMetadata.forEach((value, node) => {
    if (value.in === 0) {
      queue.enqueue(node);
    }
  });

  while (queue.length()) {
    const node = queue.dequeue();

    nodeMetadata.get(node).out.forEach((neighbor) => {
      nodeMetadata.get(neighbor).in -= 1;

      if (nodeMetadata.get(neighbor).in === 0) {
        queue.enqueue(neighbor);
      }
    });

    order.push(node);
  }

  return order.length === graphNodes.length ? order : [];
}

// or
export default function topologicalSort(graph) {
  const graphNodes = Object.keys(graph);
  const nodeMetadata = new Map();
  const queue = [];
  const order = [];

  for (const node of graphNodes) {
    nodeMetadata.set(node, {
      in: 0,
      out: new Set(graph[node]),
    });
  }

  for (const node of graphNodes) {
    for (const neighbor of graph[node]) {
      nodeMetadata.get(neighbor).in += 1;
    }
  }

  for (const [node, value] of nodeMetadata) {
    if (value.in === 0) {
      queue.push(node);
    }
  }

  while (queue.length) {
    const node = queue.shift();

    for (const neighbor of nodeMetadata.get(node).out) {
      nodeMetadata.get(neighbor).in -= 1;

      if (nodeMetadata.get(neighbor).in === 0) {
        queue.push(neighbor);
      }
    }

    order.push(node);
  }

  return order.length === graphNodes.length ? order : [];
}
```
