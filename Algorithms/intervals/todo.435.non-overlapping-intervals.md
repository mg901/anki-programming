## [435 Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)

```js
function eraseOverlapIntervals(intervals) {
  intervals.sort((a, b) => a[1] - b[1]);

  let [, prevEnd] = intervals[0];
  let count = 0;

  for (let i = 1; i < intervals.length; i += 1) {
    const [start, end] = intervals[i];

    if (prevEnd > start) {
      count += 1;
    } else {
      prevEnd = end;
    }
  }

  return count;
}
```
