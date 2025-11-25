## [1851 Minimum Interval to Include Each Query](https://leetcode.com/problems/minimum-interval-to-include-each-query/description/)

<!-- notecardId: 1747932806896 -->

```js
function minInterval(intervals, queries) {
  intervals.sort((a, b) => a[0] - b[0]);

  const sortedQueries = queries.toSorted((a, b) => a - b);
  const minpq = new MinPriorityQueue((x) => x.size);
  const querySizeMap = new Map();

  let i = 0;

  for (const query of sortedQueries) {
    while (i < intervals.length && intervals[i][0] <= query) {
      const [start, end] = intervals[i];

      minpq.enqueue({
        size: end - start + 1,
        end,
      });

      i += 1;
    }

    while (!minpq.isEmpty() && minpq.front().end < query) {
      minpq.dequeue();
    }

    querySizeMap.set(query, minpq.isEmpty() ? -1 : minpq.front().size);
  }

  return queries.map((query) => querySizeMap.get(query));
```
