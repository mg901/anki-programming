## [846 Hand of Straights](https://leetcode.com/problems/hand-of-straights/description/)

```js
function isNStraightHand(hand, groupSize) {
  if (hand.length % groupSize !== 0) return false;

  const counter = new Map();

  for (const num of hand) {
    counter.set(num, (counter.get(num) ?? 0) + 1);
  }

  hand.sort((a, b) => a - b);

  for (const num of hand) {
    const count = counter.get(num);
    if (count === 0) continue;

    for (let i = 0; i < groupSize; i += 1) {
      const current = i + num;
      const count = counter.get(current);
      if (count === 0) return false;

      counter.set(current, count - 1);
    }
  }

  return true;
}
```
