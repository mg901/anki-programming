## [Topological Sort 'Adj Matrix'](https://leetcode.com/problems/course-schedule/description/)

```js
// Algorithm:
// - Kahn's Algorithm (Topological Sort)
// - William Fiset: https://youtu.be/cIBFEhD77b4?si=VACW-ox4kQQDqfV4

// Explanation:
// - Neetcode: https://youtu.be/EgI5nU9etnU

// Complexity:
// - Time: O(V + E)
// - Space: O(V + E)
function canFinish(numCourses, prerequisites) {
  const n = numCourses;
  const graph = Array.from({ length: n }, () => []);
  const inDegree = new Array(n);
  const queue = [];
  let count = 0;

  for (const [v, u] of prerequisites) {
    graph[u].push(v);
    inDegree[v] += 1;
  }

  for (let u = 0; u < n; u += 1) {
    if (inDegree[u] === 0) {
      queue.push(u);
    }
  }

  while (queue.length) {
    const u = queue.shift();
    count += 1;

    for (const v of graph[u]) {
      inDegree[v] -= 1;

      if (inDegree[v] === 0) {
        queue.push(v);
      }
    }
  }

  return count === n;
}
```
