## [Data merging](https://www.greatfrontend.com/interviews/study/gfe75/questions/javascript/data-merging)

```js
export default function mergeData(sessions) {
  const userToData = new Map();

  for (const { user, duration, equipment } of sessions) {
    let data = userToData.get(user);

    if (!data) {
      data = {
        duration: 0,
        equipment: new Set(),
      };

      userToData.set(user, data);
    }

    data.duration += duration;

    for (const item of equipment) {
      data.equipment.add(item);
    }
  }

  return userToData
    .entries()
    .map(([user, data]) => ({
      user,
      duration: data.duration,
      equipment: Array.from(data.equipment).sort(),
    }))
    .toArray();
}
```
