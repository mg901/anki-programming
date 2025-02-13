## [Data merging](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/data-merging)

<!-- notecardId: 1739454836934 -->

```js
function mergeData(sessions) {
  const map = new Map();

  for (const session of sessions) {
    const { user, duration, equipment } = session;

    if (!map.has(user)) {
      map.set(user, {
        duration,
        equipment: new Set(equipment),
      });
    } else {
      const item = map.get(user);
      item.duration += duration;

      for (const value of equipment) {
        item.equipment.add(value);
      }
    }
  }

  const result = [];

  for (const [user, { duration, equipment }] of map) {
    result.push({
      user,
      duration,
      equipment: Array.from(equipment).sort(),
    });
  }

  return result;
}
```
