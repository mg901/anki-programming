## [Topological Sort 'Kahn Adj List'](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393169196 -->

```js
function topologicalSort(graph) {
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

## [Topological Sort 'Kahn Adj Matrix'](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393169203 -->

```js
function topologicalSort(matrix) {
  const n = matrix.length;
  const inDegree = new Uint8Array(n);
  const queue = [];
  const result = [];

  for (let u = 0; u < n; u += 1) {
    for (let v = 0; v < n; v += 1) {
      if (matrix[u][v]) {
        inDegree[v] += 1;
      }
    }
  }

  for (let u = 0; u < n; u += 1) {
    if (inDegree[u] === 0) {
      queue.push(u);
    }
  }

  while (queue.length) {
    const u = queue.shift();
    result.push(u);

    for (let v = 0; v < n; v += 1) {
      if (matrix[u][v]) {
        inDegree[v] -= 1;

        if (inDegree[v] === 0) {
          queue.push(v);
        }
      }
    }
  }

  return result.length === n ? result : [];
}
```

## [Topological Sort 'DFS Adj List'](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393169205 -->

```js
function topologicalSort(graph) {
  const nodes = Object.keys(graph);
  const visited = new Set();
  const visiting = new Set();
  const result = [];

  for (const node of nodes) {
    if (dfs(node) === false) return [];
  }

  return result.reverse();

  function dfs(node) {
    const stack = [[node, 0]];

    while (stack.length) {
      const [u, state] = stack.pop();

      if (state === 0) {
        if (visited.has(u)) continue;
        if (visiting.has(u)) return false;

        stack.push([u, 1]);
        visiting.add(u);

        for (const v of graph[u] ?? []) {
          if (!visited.has(v)) {
            stack.push([v, 0]);
          }
        }
      } else {
        visiting.delete(u);
        visited.add(u);
        result.push(u);
      }
    }

    return true;
  }
}
```

## [Topological Sort 'DFS Adj-matrix'](https://reimagined-orbit-7j4w5jq566hrv6j.github.dev/)

<!-- notecardId: 1756393169208 -->

```js
function topologicalSort(matrix) {
  const n = matrix.length;
  const visited = new Set();
  const visiting = new Set();
  const result = [];

  for (let u = 0; u < n; u += 1) {
    if (dfs(u) === false) return [];
  }

  return result.reverse();

  function dfs(node) {
    const stack = [[node, 0]];

    while (stack.length) {
      const [u, state] = stack.pop();

      if (state === 0) {
        if (visited.has(u)) continue;
        if (visiting.has(u)) return false;

        stack.push([u, 1]);
        visiting.add(u);

        for (let v = 0; v < n; v += 1) {
          if (matrix[u][v] && !visited.has(v)) {
            stack.push([v, 0]);
          }
        }
      } else {
        visiting.delete(u);
        visited.add(u);
        result.push(u);
      }
    }

    return true;
  }
}
```
