## [252 Meeting Rooms](https://neetcode.io/problems/meeting-schedule)

```js
function canAttendMeetings(intervals) {
  intervals.sort((a, b) => a.start - b.start);

  for (let i = 1; i < intervals.length; i += 1) {
    if (intervals[i - 1].end > intervals[i].start) return false;
  }

  return true;
}
```
